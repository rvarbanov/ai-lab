# ai-lab

A personal lab for experimenting with AI prompts, skills, and tools. This is a living, forever-WIP collection — the goal is to try things, keep what works, and toss what doesn't. Nothing here is meant to be polished or production-ready until it proves itself.

The secondary goal is **portability**: everything here is designed to be synced into other projects via symlinks or an install script, so you have a single source of truth for your AI toolkit across codebases.

## Overview

This repo is designed to:
- **Centralize** prompts, agent definitions, and tool configs in one place
- **Experiment** freely — half-baked ideas welcome
- **Sync** into other projects via symlinks or `install.sh`
- **Version** what works so you can reuse and iterate on it
- **Share** with teammates when something graduates from experiment to useful

## Repository Structure

```
ai-lab/
├── prompt/           # Reusable prompt templates and context docs
├── skill/            # Focused, composable capabilities
├── agent/            # Full agent definitions and system prompts
├── tool/             # Tool configs, scripts, and utilities
├── templates/        # Skeleton files for creating new prompts, skills, agents, and tools
├── wip/              # Scratch space — nothing here is precious
└── README.md
```

## Concepts

- **Prompt** — A reusable text template or instruction fragment. Stateless. You feed it input, it shapes the model's output. No persistent behavior.
- **Skill** — A focused, composable capability. A prompt + defined input/output contract. A named, reusable unit of work (e.g., "summarize a ticket", "write a commit message").
- **Agent** — A full autonomous entity with a system prompt, defined tools, decision-making loop, and often a persona. It can take multi-step actions, use tools, and run until a goal is complete. An agent *uses* prompts and skills internally.

> **Analogy:** Prompt = a recipe card. Skill = a trained technique. Agent = a chef who uses many techniques to cook a full meal.

## Lab Philosophy

This is an experiment-first repo. The rules:
- **WIP is the default state** — incomplete ideas live here too
- **Flat over nested** — don't over-structure until patterns emerge
- **Promote when proven** — things graduate to `prompt/` or `agent/` once they've earned it
- **Delete freely** — if it didn't work, remove it

## Categories

### Prompts
Reusable prompt templates and context docs:
- [`generate-readme.prompt.md`](prompt/generate-readme.prompt.md) — generate a README.md for Go projects

#### workitem/
Prompts for defining, scoping, and constraining a unit of work — use in sequence:
- [`engineer-intent.prompt.md`](prompt/workitem/engineer-intent.prompt.md) — encode purpose, values, and decision boundaries → produces `INTENT.md`
- [`engineer-specification.prompt.md`](prompt/workitem/engineer-specification.prompt.md) — write a precise, agent-executable spec → produces `SPEC.md`
- [`architect-service.prompt.md`](prompt/workitem/architect-service.prompt.md) — canonical service layer architecture rules (inject as agent context)

#### jira/
- [`acli-commands.prompt.md`](prompt/jira/acli-commands.prompt.md) — complete ACLI (Atlassian CLI) command reference
- [`review-field-filters.prompt.md`](prompt/jira/review-field-filters.prompt.md) — JIRA field filter analysis for reducing payload size
- [`filter-fields.prompt.md`](prompt/jira/filter-fields.prompt.md) — list of safe-to-filter JIRA fields
- [`build-acli-command.prompt.md`](prompt/jira/build-acli-command.prompt.md) — final recommended ACLI command with optimal field set
- [`enhance-skill.prompt.md`](prompt/jira/enhance-skill.prompt.md) — suggested enhancements for the Jira skill

### Skills
Focused, composable capabilities with defined input/output contracts:
- *(none yet)*

### Agents
Full system prompts for AI agents:
- [`jira-hydrator.agent.md`](agent/jira-hydrator.agent.md) — fetches all context for a Jira issue (epic, stories, tasks, bugs, PRs) and persists it to `workitem/{ID}/` for other agents to consume
- [`jira-retriever.agent.md`](agent/jira-retriever.agent.md) — retrieves Jira work items by ticket ID or current git branch

### Tools
Scripts, configs, and utilities that complement AI workflows:
- *(none yet)*

## Usage

### Syncing into a project

The simplest approach — symlink this repo into your project:

```bash
# From your project root
ln -s ~/path/to/ai-lab .ai

# Or run an install script (once it exists)
bash ~/path/to/ai-lab/install.sh
```

### Adding a new prompt or agent

1. Optionally start from a file in `templates/` (e.g. `my-prompt.prompt.md`) — copy it, rename, and edit.
2. Drop the file in `wip/` first while experimenting
3. Once it's working, move it to `prompt/` or `agent/` with a descriptive name following the naming convention
4. Add a one-liner to this README under the relevant category

## Naming Convention

All files follow the pattern `{name}.{type}.md` with kebab-case names.

### Types and their dirs

| Type | Dir | Extension |
|---|---|---|
| Prompt | `prompt/` | `.prompt.md` |
| Skill | `skill/` | `.skill.md` |
| Agent | `agent/` | `.agent.md` |
| Tool | `tool/` | `.tool.md` |

### Name structure

- **Prompts & skills** → `{verb}-{noun}` — they're tasks: `generate-readme`, `summarize-ticket`
- **Agents** → `{domain}-{role}` — they're personas: `jira-hydrator`, `code-reviewer`
- **Tools** → `{domain}-{verb}` — they're utilities: `jira-fetch`, `git-sync`

### Subdir rule

Create a domain subdir (e.g. `prompt/jira/`) only when **3 or more files** share the same domain. Otherwise keep flat.

### Verb shortlist

Reuse these to stay consistent: `generate`, `review`, `analyze`, `extract`, `build`, `hydrate`, `summarize`, `write`, `fetch`, `engineer`

### Examples

```
agent/jira-hydrator.agent.md
skill/summarize-ticket.skill.md
prompt/generate-readme.prompt.md
prompt/jira/build-acli-command.prompt.md
tool/jira-fetch.tool.md
```

### Glob patterns

```bash
ls agent/*.agent.md          # all agents
ls skill/*.skill.md          # all skills
ls prompt/**/*.prompt.md     # all prompts
ls tool/*.tool.md            # all tools
```

## Contributing

1. Follow the naming convention: `{name}.{type}.md` in the correct dir (see **Naming Convention** above)
2. Drop experiments in `wip/` first — promote to the right folder once proven
3. Add a one-liner to this README when promoting something
4. Delete things that didn't work — a clean repo is more useful than a full one

## Notes

- Keep prompts focused and composable
- Document quirks and limitations when you find them
- `wip/` is scratch space — nothing there is expected to be stable

