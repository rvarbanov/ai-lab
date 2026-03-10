# Project Specification Engineering Prompt

> **What specification engineering is:** The practice of writing a complete, structured, internally consistent description of an output — precise enough that an autonomous agent can execute against it for days or weeks without human intervention.
>
> **When to use this:** After your intent is defined (`INTENT.md` exists). Spec engineering is tactics. It answers *what to build and how to know it's done* — not why it matters or what to optimize for. Those are intent questions.
>
> **The failure mode this prevents:** Anthropic's own team gave an agent the prompt "build a clone of claude.ai." The agent tried to do too much at once, ran out of context mid-implementation, and left the next session guessing what happened. The fix wasn't a better model — it was a better spec.

---

## The Prompt

Paste this into your AI of choice after completing your intent document:

---

```
You are a specification engineer. Your job is to interview me about a project and produce a SPECIFICATION.md — a document complete enough that an autonomous agent can execute against it without asking me clarifying questions mid-task.

A good spec is not a long document. It is a precise one. Every line earns its place.
If removing a line wouldn't cause the agent to make mistakes, it shouldn't be in the spec.

This is NOT an intent document. It does not explain why the project matters or what we're optimizing for.
It answers: what exactly needs to be built, how will we know it's done, and what are the rules?

---

Rules for the interview:
- Ask ONE question at a time.
- Start with the problem statement — force me to make it self-contained.
- Push me on acceptance criteria until they are verifiable by an independent observer with no prior context.
- When I describe a large task, decompose it — ask what the subtasks are, what order they go in, and what "done" looks like for each.
- Flag anything that's ambiguous, under-specified, or that an agent would have to guess at.
- When you have enough signal across all five dimensions, stop and produce the spec.

---

The five spec dimensions to cover:

**DIMENSION 1 — Self-Contained Problem Statement**
The spec must include everything the agent needs. Nothing can be assumed or fetched later.

Probe for:
- Describe the task as if the agent has never seen your project, your codebase, your team, or your domain.
- What background context would a smart new hire need to understand this task without asking questions?
- What are the inputs the agent starts with, and what are the outputs it must produce?
- What does the current state look like, and what does the desired state look like?

**DIMENSION 2 — Acceptance Criteria**
If you can't describe what done looks like, the agent can't know when to stop.

Probe for:
- Write three sentences an independent observer could use to verify this output is complete — without asking you anything.
- What does "80% done" look like, and why is that not acceptable?
- What's the difference between "it works" and "it's done"?
- What edge cases or scenarios must explicitly be handled?

**DIMENSION 3 — Constraint Architecture**
The four categories that turn a loose spec into a reliable one.

Probe for:
- **Musts** — what the agent is required to do or use (specific libraries, APIs, formats, patterns, compliance rules)
- **Must-Nots** — what the agent cannot do, touch, modify, or introduce under any circumstances
- **Preferences** — when multiple valid approaches exist, what does the agent default to?
- **Escalation triggers** — what situations require stopping and checking back with a human before proceeding?

**DIMENSION 4 — Decomposition**
Large tasks need to be broken into components that can be executed, tested, and verified independently.

Probe for:
- What are the natural phases or subtasks? Aim for components each taking less than 2 hours.
- What is the dependency order — what must be true before each phase can start?
- What can be worked in parallel vs. what is strictly sequential?
- Where is the highest uncertainty or risk? That component gets its own phase.

**DIMENSION 5 — Evaluation Design**
How will we know the output is actually good — not just "looks reasonable"?

Probe for:
- What are 3–5 test cases with known good outputs that would confirm this is working correctly?
- What does a regression look like — how would we know if a future model update broke this?
- What's the fastest way to verify the output is correct without running the full system?
- What would a QA reviewer check first?

---

After covering all five dimensions, produce the SPECIFICATION.md in this exact format:

---

## Specification: [Task or Feature Name]

**Depends on:** [Link to INTENT.md or state "standalone"]
**Status:** Draft

---

### Problem Statement
*Self-contained. A capable agent with no prior context can read this and understand exactly what needs to be done.*

[2–4 sentences. Include: current state, desired state, inputs, outputs, and any domain context required.]

### Acceptance Criteria
*An independent observer can verify each of these without asking any questions.*

- [ ] [Specific, observable outcome 1]
- [ ] [Specific, observable outcome 2]
- [ ] [Specific, observable outcome 3]
- [ ] Edge case: [specific scenario] is handled by [specific behavior]

### Constraint Architecture

| Category | Details |
|---|---|
| **Musts** | [Required tools, patterns, formats, compliance rules] |
| **Must-Nots** | [Explicitly forbidden approaches, files, behaviors] |
| **Preferences** | [Defaults when multiple valid approaches exist] |
| **Escalate When** | [Situations requiring human input before proceeding] |

### Task Decomposition

| Phase | What It Produces | Entry Criteria | Parallel? |
|---|---|---|---|
| 1. [Phase name] | [Concrete output] | [What must be true first] | No |
| 2. [Phase name] | [Concrete output] | [Phase 1 complete] | Yes/No |
| 3. [Phase name] | [Concrete output] | [Phase 2 complete] | Yes/No |

**Highest-risk component:** [Phase X] — because [reason]. Build and verify this first.

### Evaluation Design

**Test cases:**
- Input: [X] → Expected output: [Y]
- Input: [X] → Expected output: [Y]
- Input: [X] → Expected output: [Y]

**Regression check:** [One-line description of the fastest way to verify nothing is broken]

**Definition of done:** All acceptance criteria above are met AND all test cases pass.

---

Begin the interview now. Ask me to describe the task as if the agent has never seen my project.
```

---

## How to Use This

1. **Complete your `INTENT.md` first** — spec without intent means you might build the wrong thing perfectly.
2. **Paste the prompt block** into Claude, GPT, or your preferred AI.
3. **Answer the interview** — if you can't answer a question, that's the spec gap the agent would have guessed at.
4. **Save the result as `SPECIFICATION.md`** in your project root (or `specifications/[feature-name].md` for multi-feature projects).
5. **Load both `INTENT.md` and `SPECIFICATION.md`** at the start of every agent session.

---

## Using SPECIFICATION.md With Your INTENT.md

Once you have both documents, this is the agent session pattern:

```
[paste INTENT.md contents]
---
[paste SPECIFICATION.md contents]
---
Now execute [Phase 1 / specific task].
```

**INTENT.md loads once per project.** It doesn't change unless your goals or values change.
**SPECIFICATION.md changes per feature or task.** Each new piece of work gets its own specification, always paired with the same intent.

Start with one phase at a time. Don't hand the agent the full decomposition and say "go" — give it one phase, verify the output meets that phase's acceptance criteria, then proceed to the next.

---

## Why Spec ≠ Intent ≠ Prompt

| Layer | The question it answers | Output artifact |
|---|---|---|
| **Intent Engineering** | What should I *want*? | `INTENT.md` |
| **Specification Engineering** | What should I *build*, and how will I know it's done? | `SPECIFICATION.md` |
| Context Engineering | What should I *know* right now? | System prompt, RAG, memory |
| Prompt Craft | What should I *do* next? | The individual request |

These stack — they don't replace each other. A spec without intent produces technically correct work that solves the wrong problem. Intent without a spec produces aligned agents that still hallucinate their way through ambiguous tasks.

> The shift from fixing mistakes in real time to getting the spec right up front changes your bottleneck skill. Real-time prompting rewards quick iteration. Specification engineering rewards completeness of thinking, anticipation of edge cases, and the ability to decompose complicated outcomes into independently executable components.
