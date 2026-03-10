# workitem/

Prompts for defining, scoping, and constraining a unit of work — from raw idea to agent-executable spec.

Use these in sequence before an agent (or teammate) touches the implementation.

---

## Workflow

### 1. Intent → [`project-intent-engineering-prompt.md`](project-intent-engineering-prompt.md)
**Start here.** Before writing a single line of spec or code.

Encodes *why* the work matters, what to optimize for, and how to make judgment calls when things conflict. The output is an `INTENT.md` — a lightweight artifact any agent or new contributor can read to understand what the project is *for*.

> No spec or agent should run without intent defined first.

### 2. Spec → [`project-spec-engineering-prompt.md`](project-spec-engineering-prompt.md)
**After intent is defined.**

Produces a `SPEC.md` — precise enough that an autonomous agent can execute against it for days without asking clarifying questions. Focuses on *what* to build and *how to know it's done*, not why it matters.

> A good spec is not long. It is precise. Every line earns its place.

### 3. Architecture → [`service-architect-spec.md`](service-architect-spec.md)
**Inject as agent context when making code changes.**

Defines the canonical layer architecture for the service. AI agents making code changes must follow these rules and must not introduce violations. Reference this alongside the spec so the agent knows not just *what* to build but *how* to structure it.

---

## Summary

| Step | File | Output | Question answered |
|------|------|--------|-------------------|
| 1 | `project-intent-engineering-prompt.md` | `INTENT.md` | What should we want? |
| 2 | `project-spec-engineering-prompt.md` | `SPEC.md` | What exactly needs to be built? |
| 3 | `service-architect-spec.md` | (agent context) | How must the code be structured? |
