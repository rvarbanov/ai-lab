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
├── prompts/          # Reusable prompts organized by category
├── agents/           # Full agent definitions and system prompts
├── tools/            # Tool configs, scripts, and utilities
├── memory-bank/      # Persistent context and reference docs
├── tmp/              # Scratch space — nothing here is precious
└── README.md
```

## Lab Philosophy

This is an experiment-first repo. The rules:
- **WIP is the default state** — incomplete ideas live here too
- **Flat over nested** — don't over-structure until patterns emerge
- **Promote when proven** — things graduate to `prompts/` or `agents/` once they've earned it
- **Delete freely** — if it didn't work, remove it

## Categories

### Prompts
Reusable prompt fragments and templates:
- Purpose and use case
- Input parameters (if any)
- Expected output format
- Known limitations

### Agents
Full system prompts for AI agents:
- Agent description and capabilities
- Required tools or integrations
- Example interactions

### Tools
Scripts, configs, and utilities that complement AI workflows:
- What it does
- How to use it
- Dependencies

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

