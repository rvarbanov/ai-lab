# Service Architecture Spec

This document defines the canonical layer architecture for this service. AI agents making code changes **must follow these rules** and **must not introduce violations**.

---

## Two Patterns — Choose Based on Complexity

### Pattern A: Simple CRUD (no pipeline)

Use when the operation is a straightforward create, read, update, or delete with no multi-step pipeline logic.

**Decision criteria:** Does the operation require loading external data, validating against business rules across multiple entities, syncing state, AND persisting atomically? **No** → use Pattern A.

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   HTTP Handler  │    │ Event Consumer  │    │ Batch Job       │
│  (web/server/)  │    │  (async/)       │    │  (jobs/)        │
└────────┬────────┘    └────────┬────────┘    └────────┬────────┘
         │                      │                      │
         └──────────────────────┼──────────────────────┘
                                │
                    ┌───────────▼───────────┐
                    │        Manager        │  ← business rules + orchestration
                    │     (services/)       │
                    └──────────┬────────────┘
                               │
               ┌───────────────┼───────────────┐
               │               │               │
    ┌──────────▼──────┐  ┌─────▼─────┐  ┌──────▼──────────────┐
    │      Repo       │  │  Client   │  │   Event Producer    │
    │    (repo/)      │  │ (client/) │  │    (async/)         │
    └─────────────────┘  └───────────┘  └─────────────────────┘
```

**Examples:** get claim adjustment by ID, list mass reversal requests, create an adj pool, delete an exclusion.

---

### Pattern B: Complex Pipeline (load → validate → sync → persist)

Use when the operation requires multiple coordinated steps: fetching data from multiple sources, applying cross-entity validation, reconciling state, and persisting atomically.

**Decision criteria:** Does the operation require loading external data, validating against business rules across multiple entities, syncing state, AND persisting atomically? **Yes** → use Pattern B.

```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   HTTP Handler  │    │ Event Consumer  │    │ Batch Job       │
│  (web/server/)  │    │  (async/)       │    │  (jobs/)        │
└────────┬────────┘    └────────┬────────┘    └────────┬────────┘
         │                      │                      │
         └──────────────────────┼──────────────────────┘
                                │
                    ┌───────────▼───────────┐
                    │       Processor       │  ← orchestrates the pipeline
                    │    (services/engine/) │     load → validate → sync → persist
                    └──────────┬────────────┘
                               │  (calls Manager for each stage)
                    ┌──────────▼────────────┐
                    │        Manager        │  ← domain/business rules per stage
                    │     (services/)       │
                    └──────────┬────────────┘
                               │
               ┌───────────────┼───────────────┐
               │               │               │
    ┌──────────▼──────┐  ┌─────▼─────┐  ┌──────▼──────────────┐
    │      Repo       │  │  Client   │  │   Event Producer    │
    │    (repo/)      │  │ (client/) │  │    (async/)         │
    └─────────────────┘  └───────────┘  └─────────────────────┘
```

**Examples:** process a claim adjustment (load claim + existing adj, validate thresholds, sync status, persist), process a mass reversal row.

---

## Layer Responsibilities

### Entry Points (Handler, Consumer, Job)
- Parse and validate the incoming request/message/trigger (HTTP, Kafka, schedule)
- Call either the **Processor** (for complex flows) or the **Manager** (for simple CRUD)
- Return/publish the response or acknowledgement
- **Must not** contain business logic
- **Must not** call Repo directly
- **Must not** call Producer directly

### Processor (`services/engine/`)
- Owns the use-case pipeline: **load → validate → sync → persist**
- Sub-packages (`loader/`, `validator/`, `sync/`, `persist/`) are internal pipeline stages, not separate layers
- Calls **Manager** for domain rules and data access — **not Repo directly**
- Returns a result to the caller; does **not** emit events or call Producers
- **Must not** be called by Manager (no upward calls)

### Manager (`services/`)
- Encapsulates domain/business rules for a single entity or bounded context
- Called by Processor pipeline stages, or directly by entry points for simple CRUD
- May call **Repo**, **Client**, and **Producer**
- May call another Manager **only for true cross-domain orchestration** (e.g. validating a foreign entity before creating a record). For pure data lookups across domains, inject the Repo instead.
- **Must not** call Processor (no downward-then-upward cycles)

### Repo (`repo/`)
- SQL queries and data access only
- No business logic, no cross-entity joins that encode business rules
- Called by Manager only

### Client (`services/client/`)
- External service integrations (MDM, Claims, DMS, ACM, Provider)
- Called by Manager only

### Event Producer (`async/producer/`)
- Publishes domain events to Kafka
- Called by Manager only — after business logic completes
- **Must not** be called by Processor

### Event Consumer (`async/consumer/`)
- Receives Kafka messages
- Calls Processor or Manager — same rules as Handler

---

## Rules (Enforce on Every Code Change)

| Rule | Allowed | Forbidden |
|---|---|---|
| Entry point calls | Processor, Manager | Repo, Producer, Client |
| Processor calls | Manager | Repo directly, Producer, another Processor |
| Manager calls | Repo, Client, Producer, (other Manager sparingly) | Processor |
| Repo calls | DB only | anything above |
| Producer calls | Kafka only | anything above |

### Manager → Manager guidance
- ✅ Allowed: calling another Manager to enforce a cross-domain business rule (e.g. "does this mass adj exist and is it eligible?")
- ✅ Allowed: calling another Manager to write a linked record as part of one atomic operation
- ❌ Avoid: calling another Manager purely to read data — inject the Repo instead
- ❌ Never: circular Manager → Manager → Manager chains

---

## Known Violations (Do Not Replicate)

The following patterns exist in the codebase today and are **legacy violations**. Do not replicate them in new code. Fix them when touching the relevant files.

| Location | Violation | Rule Broken |
|---|---|---|
| `web/server/server.go` | `claimAdjProcessor`, `claimAdjStatusProcessor`, `massExclInclProcessor` injected into `IntAdjApis` | Entry point must not hold Processor directly |
| `web/server/claim_adj.go` | Handler calls `ia.claimAdjProcessor.ProcessClaimAdj()` | Entry point → Processor (bypass Manager) |
| `web/server/claim_adj_rev.go` | Handler calls `ia.claimAdjFactory.GetAdjPostProcessor().Process()` | Entry point dispatching Processor via factory |
| `web/server/adj_excl.go` | Handler calls `ia.massExclInclProcessor.Process()` | Entry point → Processor (bypass Manager) |
| `services/engine/loader/*.go` | Loader sub-packages inject `*Mgr` types | Processor pipeline should call Manager, not hold it as a field in sub-packages — make the dependency explicit at Processor level |
| `services/engine/persist/*.go` | Persist sub-packages inject `*Mgr` types | Same as above |
| `services/engine/validator/*.go` | Validator sub-packages inject `*Mgr` types | Same as above |
| `services/engine/claim_adj_status_processor.go` | Holds `batchProducerMgr` and emits events | Processor must not call Producer |
| `services/engine/upload_file_processor.go` | Holds `UploadFileMgr`, `MassAdjUploadRowsMgr` directly | Manager dependency should be at Processor level, not in sub-packages |
| `services/mass_adj_upload_mgr.go` | Injects `MassAdjMgr` but never uses it | Dead injection — remove |
| `services/adj_exec_pool_run_hist_rpt_mgr.go` | Holds `AdjExecPoolRunHistMgr` for a single read call | Pure lookup — inject Repo instead |

---

## Adding New Features — Checklist

- [ ] Decide pattern: does the operation need load + validate + sync + persist? → **Pattern B (Processor)**. Otherwise → **Pattern A (Manager only)**
- [ ] Entry point (handler/consumer/job) calls Processor (Pattern B) or Manager (Pattern A) — never Repo/Producer/Client directly
- [ ] Processor stages (loader/validator/persist) call Manager for business rules, not Repo
- [ ] Manager emits events via Producer after business logic completes
- [ ] New Manager → Manager dependency: confirm it's cross-domain orchestration, not a data lookup
- [ ] Wire up new dependencies in `wire.go` and run `go generate ./...`
- [ ] Add mocks for any new interfaces under `test/mock/`
