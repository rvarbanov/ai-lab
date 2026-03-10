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
├── prompts/          # Reusable prompt templates and context docs
├── skills/           # Focused, composable capabilities
├── agents/           # Full agent definitions and system prompts
├── tools/            # Tool configs, scripts, and utilities
├── tmp/              # Scratch space — nothing here is precious
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
- **Promote when proven** — things graduate to `prompts/` or `agents/` once they've earned it
- **Delete freely** — if it didn't work, remove it

## Categories

### Prompts
Reusable prompt templates and context docs:
- [`readme-md-generator-prompt.md`](prompts/readme-md-generator-prompt.md) — generate a README.md for Go projects

#### workitem/
Prompts for defining, scoping, and constraining a unit of work — use in sequence:
- [`project-intent-engineering-prompt.md`](prompts/workitem/project-intent-engineering-prompt.md) — encode purpose, values, and decision boundaries → produces `INTENT.md`
- [`project-spec-engineering-prompt.md`](prompts/workitem/project-spec-engineering-prompt.md) — write a precise, agent-executable spec → produces `SPEC.md`
- [`service-architect-spec.md`](prompts/workitem/service-architect-spec.md) — canonical service layer architecture rules (inject as agent context)

#### jira/
- [`acli-commands.md`](prompts/jira/acli-commands.md) — complete ACLI (Atlassian CLI) command reference
- [`field-filter-review.md`](prompts/jira/field-filter-review.md) — JIRA field filter analysis for reducing payload size
- [`fields-to-filter.md`](prompts/jira/fields-to-filter.md) — list of safe-to-filter JIRA fields
- [`filtered-acli-command.md`](prompts/jira/filtered-acli-command.md) — final recommended ACLI command with optimal field set

### Skills
Focused, composable capabilities with defined input/output contracts:
- *(none yet)*

### Agents
Full system prompts for AI agents:
- [`jira-context-hydrator-agent.md`](agents/jira-context-hydrator-agent.md) — fetches all context for a Jira issue (epic, stories, tasks, bugs, PRs) and persists it to `workitem/{ID}/` for other agents to consume
- [`jira-workitem-retriever-agent.md`](agents/jira-workitem-retriever-agent.md) — retrieves Jira work items by ticket ID or current git branch

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

1. Drop the file in `tmp/` first while experimenting
2. Once it's working, move it to `prompts/` or `agents/` with a descriptive name
3. Add a one-liner to this README under the relevant category

## Contributing

1. Follow naming conventions: lowercase with hyphens (`my-prompt.md`)
2. Drop experiments in `tmp/` first — promote to the right folder once proven
3. Add a one-liner to this README when promoting something
4. Delete things that didn't work — a clean repo is more useful than a full one

## Notes

- Keep prompts focused and composable
- Document quirks and limitations when you find them
- `tmp/` is scratch space — nothing there is expected to be stable

