# prompts/jira

JIRA-related prompts, reference docs, and context for AI agents working with Jira tickets and the ACLI tool.

## Files

| File | Description |
|------|-------------|
| [`acli-commands.md`](acli-commands.md) | Complete ACLI (Atlassian CLI) command reference |
| [`field-filter-review.md`](field-filter-review.md) | Deep analysis of 200+ JIRA fields — what to keep, what to exclude, and why |
| [`fields-to-filter.md`](fields-to-filter.md) | Quick-reference list of safe-to-filter fields with recommended filtered commands |
| [`filtered-acli-command.md`](filtered-acli-command.md) | Final verified ACLI command with the optimal field set (`*navigable,attachment`) |
| [`jira-skill-enhancements.md`](jira-skill-enhancements.md) | JIRA story section weights + epic context gathering strategy for agents |

## Related Agents

| Agent | Description |
|-------|-------------|
| [`jira-context-hydrator-agent`](../../agents/jira-context-hydrator-agent.md) | Given an issue ID, fetches all related context (epic, stories, tasks, bugs, PRs) and writes it to `workitem/{ID}/` locally for other agents to consume |
| [`jira-workitem-retriever-agent`](../../agents/jira-workitem-retriever-agent.md) | Lightweight retrieval — fetches and displays a single Jira ticket |

## Usage

- **Fetching a ticket**: Use [`filtered-acli-command.md`](filtered-acli-command.md) for the recommended command. It strips payload bloat while keeping all fields that matter.
- **Tuning agent behavior**: Feed [`jira-skill-enhancements.md`](jira-skill-enhancements.md) to an agent to teach it how to prioritize and interpret JIRA story sections (Tech Details > AC > Comments > Description > Title).
- **Understanding field decisions**: [`field-filter-review.md`](field-filter-review.md) explains the reasoning; [`fields-to-filter.md`](fields-to-filter.md) is the fast lookup version.
