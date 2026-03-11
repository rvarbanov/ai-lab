# Prompts

## Four disciplines of prompting (2026)

One prompt file per skill. Copy the contents (Role through Constraints) into your AI chat, then provide the context it asks for.

### 1. Prompt Craft (synchronous, session-based)

| # | File | Purpose |
|---|------|---------|
| 1.1 | [prompt-craft/01-one-shot-request-builder.md](prompt-craft/01-one-shot-request-builder.md) | Turn a rough goal into one well-structured request |
| 1.2 | [prompt-craft/02-counter-examples-ambiguity-resolver.md](prompt-craft/02-counter-examples-ambiguity-resolver.md) | Harden a prompt with counter-examples and ambiguity rules |
| 1.3 | [prompt-craft/03-output-format-guardrails-definer.md](prompt-craft/03-output-format-guardrails-definer.md) | Define output format and guardrails for a task |
| 1.4 | [prompt-craft/04-prompt-iteration-quality-reviewer.md](prompt-craft/04-prompt-iteration-quality-reviewer.md) | Compare output to intent and suggest prompt edits |

### 2. Context Engineering (curating the token environment)

| # | File | Purpose |
|---|------|---------|
| 2.1 | [context-engineering/01-project-context-file-designer.md](context-engineering/01-project-context-file-designer.md) | Design .claude.md / agent context file |
| 2.2 | [context-engineering/02-context-window-curator.md](context-engineering/02-context-window-curator.md) | Choose what to include/exclude for a single task |
| 2.3 | [context-engineering/03-rag-retrieval-strategy.md](context-engineering/03-rag-retrieval-strategy.md) | Design RAG/retrieval strategy for an agent |
| 2.4 | [context-engineering/04-context-audit.md](context-engineering/04-context-audit.md) | Audit context for relevance and bloat |

### 3. Intent Engineering (what the agent should “want”)

| # | File | Purpose |
|---|------|---------|
| 3.1 | [intent-engineering/01-goals-values-encoder.md](intent-engineering/01-goals-values-encoder.md) | Encode goals and values for an agent |
| 3.2 | [intent-engineering/02-decision-boundaries-escalation-triggers.md](intent-engineering/02-decision-boundaries-escalation-triggers.md) | Define autonomy and escalation |
| 3.3 | [intent-engineering/03-organizational-strategy-agent-objectives.md](intent-engineering/03-organizational-strategy-agent-objectives.md) | Translate strategy into agent objectives |
| 3.4 | [intent-engineering/04-misalignment-prevention-checklist.md](intent-engineering/04-misalignment-prevention-checklist.md) | Claro-style misalignment prevention |
| 3.5 | [intent-engineering/05-intent-file-from-clarifying-questions.md](intent-engineering/05-intent-file-from-clarifying-questions.md) | Elicit intent via clarifying questions and produce an intent file for a downstream agent |

### 4. Specification Engineering (agent-executable docs)

| # | File | Purpose |
|---|------|---------|
| 4.1 | [specification-engineering/01-self-contained-problem-statement.md](specification-engineering/01-self-contained-problem-statement.md) | Write self-contained problem statements |
| 4.2 | [specification-engineering/02-acceptance-criteria-writer.md](specification-engineering/02-acceptance-criteria-writer.md) | Write acceptance criteria for delegated tasks |
| 4.3 | [specification-engineering/03-constraint-architecture-builder.md](specification-engineering/03-constraint-architecture-builder.md) | Build must / must-not / prefer / escalate |
| 4.4 | [specification-engineering/04-task-decomposition.md](specification-engineering/04-task-decomposition.md) | Decompose long-running or multi-session work |

---

## Other prompts

- [meta-prompt-create-new-prompts.md](meta-prompt-create-new-prompts.md) — Meta-prompt to create new prompts (ask clarifying questions first, then output a ready-to-use prompt).
