# ACLI Commands Documentation

Complete reference for all Atlassian CLI (acli) commands, organized by category.

## Table of Contents

- [Jira Commands](#jira-commands)
- [Admin Commands](#admin-commands)
- [Rovo Dev Commands](#rovo-dev-commands)
- [Utility Commands](#utility-commands)

---


## Jira Commands

### acli jira

Jira Cloud commands.

| Command | Description |
|---------|-------------|
| `acli jira auth` | Authenticate to use Atlassian CLI |
| `acli jira board` | Jira board commands |
| `acli jira dashboard` | Jira dashboard commands |
| `acli jira field` | Jira field commands |
| `acli jira filter` | Jira filter commands |
| `acli jira project` | Jira project commands |
| `acli jira sprint` | Jira sprint commands |
| `acli jira workitem` | Jira work item commands |

### acli jira auth

Authenticate to use Atlassian CLI.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira auth login` | Authenticate with an Atlassian host | `-e, --email string`, `-s, --site string`, `--token`, `-w, --web` |
| `acli jira auth logout` | Logout from account | None |
| `acli jira auth status` | Show account status | None |
| `acli jira auth switch` | Switch between Jira accounts | `-e, --email string`, `-s, --site string` |

**Examples:**
```bash
# Authenticate using web browser (OAuth)
acli jira auth login --web

# Authenticate with email, site and API token
acli jira auth login --site "mysite.atlassian.net" --email "user@atlassian.com" --token < token.txt

# Switch accounts
acli jira auth switch --site mysite.atlassian.net --email user@atlassian.com
```

### acli jira board

Jira board commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira board get` | Jira get board details | `--id string`, `--json` |
| `acli jira board list-sprints` | Get all sprints | `--csv`, `--id string`, `--json`, `--limit int` (default 50), `--paginate`, `--state string` |
| `acli jira board search` | Search through all the boards | `--csv`, `--filter string`, `--json`, `--limit int` (default 50), `--name string`, `--orderBy string`, `--paginate`, `--private`, `--project string`, `--type string` |

**Examples:**
```bash
# Get board details
acli jira board get --id 123

# Get all sprints
acli jira board list-sprints --id 123 --state active,closed --json

# Search boards
acli jira board search --type scrum --project TEAM
```

### acli jira dashboard

Jira dashboard commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira dashboard search` | Searches for Jira dashboards | `--csv`, `-l, --limit int` (default 30), `-n, --name string`, `-e, --owner string`, `--paginate`, `--json` |

**Examples:**
```bash
# Search dashboards
acli jira dashboard search
acli jira dashboard search --paginate --csv
acli jira dashboard search --owner user@atlassian.com --name 'report'
```

### acli jira field

Jira field commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira field cancel-delete` | Restores the field from the trash | `--id string` |
| `acli jira field create` | Create a custom field in Jira | `--description string`, `--name string`, `--searcherKey string`, `--type string`, `--json` |
| `acli jira field delete` | Moves a custom field to trash | `--id string` |

**Examples:**
```bash
# Create a text field
acli jira field create --name "Customer Name" --type "com.atlassian.jira.plugin.system.customfieldtypes:textfield"

# Restore field from trash
acli jira field cancel-delete --id customfield_12345
```

### acli jira filter

Jira filter commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira filter add-favourite` | Add a filter as favourite | `--filterId string` |
| `acli jira filter change-owner` | Change the owner of the provided filters | `-f, --from-file string`, `--id string`, `--ignore-errors`, `--json`, `--owner string` |
| `acli jira filter get` | Retrieve a Jira filter by its ID | `--id string`, `--json`, `--web` |
| `acli jira filter get-columns` | Get configured columns for a filter | `--key string`, `--json` |
| `acli jira filter list` | List filter that are either my or favourite | `--favourite`, `--json`, `--my` |
| `acli jira filter reset-columns` | Reset configured columns for a filter | `--id string` |
| `acli jira filter search` | Searches for Jira filters | `--csv`, `-l, --limit int` (default 30), `-n, --name string`, `-e, --owner string`, `--paginate`, `--json` |

**Examples:**
```bash
# Add filter as favourite
acli jira filter add-favourite --filterId 10001

# Change filter owner
acli jira filter change-owner --id 123,1234,12345 --owner anna@pandora.com

# Get filter
acli jira filter get --id 12345 --web
```

### acli jira project

Jira project commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira project archive` | Archives a Jira project | `--key string` |
| `acli jira project create` | Create a Jira project – a collection of work items | `-d, --description string`, `-j, --from-json string`, `-f, --from-project string`, `-g, --generate-json`, `-k, --key string`, `-l, --lead-email string`, `-n, --name string`, `-u, --url string` |
| `acli jira project delete` | Deletes a Jira project | `--key string` |
| `acli jira project list` | List of projects visible to the user | `--json`, `-l, --limit int` (default 30), `--paginate`, `--recent` |
| `acli jira project restore` | Restore a Jira project | `--key string` |
| `acli jira project update` | Update a Jira project | `-d, --description string`, `-j, --from-json string`, `-g, --generate-json`, `-k, --key string`, `-l, --lead-email string`, `-n, --name string`, `-p, --project-key string`, `-u, --url string` |
| `acli jira project view` | Fetches a Jira project | `-j, --json`, `--key string` |

**Examples:**
```bash
# Create project from existing
acli jira project create --from-project "TEAM" --key "NEWTEAM" --name "New Project"

# List projects
acli jira project list --paginate
acli jira project list --limit 50 --json

# Archive project
acli jira project archive --key "TEAM"
```

### acli jira sprint

Jira sprint commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira sprint list-workitems` | List work items in a sprint | `--board int` (required), `--csv`, `--fields string`, `--jql string`, `--json`, `--limit int` (default 50), `--paginate`, `--sprint int` (required) |

**Examples:**
```bash
# List work items in sprint
acli jira sprint list-workitems --sprint 1 --board 6
```

### acli jira workitem

Jira work item commands.

| Command | Description |
|---------|-------------|
| `acli jira workitem archive` | Archives a work item or multiple work items |
| `acli jira workitem assign` | Assign a work item(s) to an assignee(s) |
| `acli jira workitem attachment` | Work item attachments commands |
| `acli jira workitem clone` | Create a duplicate work item(s) |
| `acli jira workitem comment` | Work item comments commands |
| `acli jira workitem create` | Create a Jira work item |
| `acli jira workitem create-bulk` | Bulk create Jira issues |
| `acli jira workitem delete` | Delete a work item or multiple work items |
| `acli jira workitem edit` | Edit a Jira work item or multiple work items |
| `acli jira workitem link` | Link work items commands |
| `acli jira workitem search` | Searches for work item or multiple work items |
| `acli jira workitem transition` | Transitioning a work item |
| `acli jira workitem unarchive` | Unarchives work item or multiple work items |
| `acli jira workitem view` | Retrieve information about Jira work items |
| `acli jira workitem watcher` | Work item watcher commands |

#### acli jira workitem archive

Archives a work item or multiple work items.

**Flags:** `--filter string`, `-f, --from-file string`, `--ignore-errors`, `--jql string`, `--json`, `-k, --key string`, `-y, --yes`

**Examples:**
```bash
acli jira workitem archive --key "KEY-1,KEY-2"
acli jira workitem archive --jql "project = TEAM"
acli jira workitem archive --filter 10001
```

#### acli jira workitem assign

Assign a work item to an assignee or multiple work items to multiple assignees.

**Flags:** `-a, --assignee string`, `--filter string`, `-f, --from-file string`, `--ignore-errors`, `--jql string`, `--json`, `-k, --key string`, `--remove-assignee`, `-y, --yes`

**Examples:**
```bash
acli jira workitem assign --key "KEY-1" --assignee "@me"
acli jira workitem assign --jql "project = TEAM" --assignee "user@atlassian.com"
```

#### acli jira workitem attachment

Work item attachments commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira workitem attachment delete` | Delete an attachment from a workitem | `--id string` |
| `acli jira workitem attachment list` | List all the attachments of a workitem | `--json`, `--key string` |

**Examples:**
```bash
acli jira workitem attachment delete --id 12345
acli jira workitem attachment list --key TEST-123
```

#### acli jira workitem clone

Create a duplicate of a work item or multiple work items.

**Flags:** `--filter string`, `-f, --from-file string`, `--ignore-errors`, `--jql string`, `--json`, `-k, --key string`, `--to-project string`, `--to-site string`, `-y, --yes`

**Examples:**
```bash
acli jira workitem clone --key "KEY-1,KEY-2" --to-project "TEAM"
```

#### acli jira workitem comment

Work item comments commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira workitem comment create` | Create a comment on work items | `-b, --body string`, `-F, --body-file string`, `-e, --edit-last`, `--editor`, `--filter string`, `--ignore-errors`, `--jql string`, `--json`, `-k, --key string` |
| `acli jira workitem comment delete` | Delete a comment for a given workitem | `--id string`, `--key string` |
| `acli jira workitem comment list` | List comments for a work item | `--json`, `--key string`, `--limit int` (default 50), `--order string` (default "+created"), `--paginate` |
| `acli jira workitem comment update` | Update a comment on a work item | `-b, --body string`, `--body-adf string`, `-F, --body-file string`, `--id string`, `--key string`, `--notify`, `--visibility-group string`, `--visibility-role string` |
| `acli jira workitem comment visibility` | Get visibility options for work item comments | `--group`, `--project string`, `--role` |

**Examples:**
```bash
acli jira workitem comment create --key "KEY-1" --body "This is a comment"
acli jira workitem comment list --key TEST-123
acli jira workitem comment update --key TEST-123 --id 10001 --body "Updated comment text"
```

#### acli jira workitem create

Create a Jira work item to track individual pieces of work.

**Flags:** `-a, --assignee string`, `-d, --description string`, `--description-file string`, `-e, --editor`, `-f, --from-file string`, `--from-json string`, `--generate-json`, `--json`, `-l, --label strings`, `--parent string`, `-p, --project string`, `-s, --summary string`, `-t, --type string`

**Examples:**
```bash
acli jira workitem create --summary "New Task" --project "TEAM" --type "Task"
acli jira workitem create --from-json "workitem.json"
```

#### acli jira workitem create-bulk

Bulk create Jira issues.

**Flags:** `--from-csv string`, `--from-json string`, `--generate-json`, `--ignore-errors`, `--yes`

**Examples:**
```bash
acli jira workitem create-bulk --from-json issues.json
acli jira workitem create-bulk --from-csv issues.csv
```

#### acli jira workitem delete

Delete a work item or multiple work items.

**Flags:** `--filter string`, `-f, --from-file string`, `--ignore-errors`, `--jql string`, `--json`, `-k, --key string`, `-y, --yes`

**Examples:**
```bash
acli jira workitem delete --key "KEY-1,KEY-2"
acli jira workitem delete --jql "project = TEAM"
```

#### acli jira workitem edit

Edit a Jira work item or multiple work items.

**Flags:** `-a, --assignee string`, `-d, --description string`, `--description-file string`, `--filter string`, `--from-json string`, `--generate-json`, `--ignore-errors`, `--jql string`, `--json`, `-k, --key string`, `-l, --labels string`, `--remove-assignee`, `--remove-labels string`, `-s, --summary string`, `-t, --type string`, `-y, --yes`

**Examples:**
```bash
acli jira workitem edit --key "KEY-1,KEY-2" --summary "New Summary"
acli jira workitem edit --from-json "workitem.json"
```

#### acli jira workitem link

Link work items commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira workitem link create` | Create links between work items | `--from-csv string`, `--from-json string`, `--generate-json`, `--ignore-errors`, `--in string`, `--out string`, `--type string`, `--yes` |
| `acli jira workitem link delete` | Delete links between work items | `--from-csv string`, `--from-json string`, `--id string`, `--ignore-errors`, `--yes` |
| `acli jira workitem link list` | List all the links of a workitem | `--json`, `--key string` |
| `acli jira workitem link type` | Get available workitem link types | `--json` |

**Examples:**
```bash
acli jira workitem link create --out KEY-123 --in KEY-456 --type Blocks
acli jira workitem link list --key TEST-123
```

#### acli jira workitem search

Searches for work item or multiple work items.

**Flags:** `--count`, `--csv`, `-f, --fields string`, `--filter string`, `-j, --jql string`, `--json`, `-l, --limit int`, `--paginate`, `-w, --web`

**Examples:**
```bash
acli jira workitem search --jql "project = TEAM" --paginate
acli jira workitem search --jql "project = TEAM" --fields "key,summary,assignee" --csv
```

#### acli jira workitem transition

Transitioning a work item to another status.

**Flags:** `--filter string`, `--ignore-errors`, `--jql string`, `--json`, `-k, --key string`, `-s, --status string`, `-y, --yes`

**Examples:**
```bash
acli jira workitem transition --key "KEY-1,KEY-2" --status "Done"
acli jira workitem transition --jql "project = TEAM" --status "In Progress"
```

#### acli jira workitem unarchive

Unarchives work item or multiple work items.

**Flags:** `-f, --from-file string`, `--ignore-errors`, `--json`, `-k, --key string`, `-y, --yes`

**Examples:**
```bash
acli jira workitem unarchive --key "KEY-1,KEY-2"
```

#### acli jira workitem view

Retrieve information about Jira work items.

**Usage:** `acli jira workitem view [key] [flags]`

**Flags:**

| Flag | Description |
|------|-------------|
| `-f, --fields string` | A list of fields to return for the work item. Accepts a comma-separated list. Use it to retrieve a subset of fields. <br><br>**Allowed values:**<br>- `*all` - returns all fields<br>- `*navigable` - returns navigable fields (fields that can be displayed as columns in the Jira issue navigator)<br>- Any work item field, prefixed with a minus to exclude<br><br>**Note:** "Navigable" fields are those that can be displayed as columns in the issue navigator, allowing for customized views and reports. This is different from "orderable" fields which can be placed on screens (like issue creation/editing screens).<br><br>**Default:** `key,issuetype,summary,status,assignee,description` |
| `--json` | Generate a JSON output |
| `-w, --web` | View the work item in the web browser |
| `-h, --help` | Show help for command |

**Field Selection Examples:**

The `--fields` flag supports flexible field selection:

```bash
# Return only specific fields
acli jira workitem view KEY-123 --fields summary,comment

# Return all fields
acli jira workitem view KEY-123 --fields "*all"

# Return all navigable fields
acli jira workitem view KEY-123 --fields "*navigable"

# Return default fields except description (exclude with minus prefix)
acli jira workitem view KEY-123 --fields "-description"

# Return all navigable fields except comment
acli jira workitem view KEY-123 --fields "*navigable,-comment"
```

**General Examples:**
```bash
# View work item with default fields
acli jira workitem view KEY-123

# View work item with specific fields
acli jira workitem view KEY-123 --fields summary,comment

# View work item in JSON format
acli jira workitem view KEY-123 --json

# View work item in web browser
acli jira workitem view KEY-123 --web

# View work item with all fields in JSON format
acli jira workitem view KEY-123 --fields "*all" --json
```

**Discovering Available Fields:**

To get a complete list of fields available for a work item, you have several options:

1. **View all fields for a specific work item:**
   ```bash
   # Get all fields for a work item (shows field names in the output)
   acli jira workitem view KEY-123 --fields "*all" --json
   ```
   This will return all fields available for that specific work item, including their field IDs and names.

2. **View all navigable fields:**
   ```bash
   # Get all navigable fields
   acli jira workitem view KEY-123 --fields "*navigable" --json
   ```
   This returns only fields that can be displayed as columns in the issue navigator.

3. **Use Jira REST API to get all fields:**
   ```bash
   # Using curl (replace with your Jira instance and credentials)
   curl -u your_email:your_api_token \
        -X GET \
        -H "Content-Type: application/json" \
        https://your_instance.atlassian.net/rest/api/3/field
   ```
   This returns a JSON array of all system and custom fields in your Jira instance, including field IDs (like `customfield_12345`) and field names.

**Note:** Field names in the `--fields` parameter can be specified by:
- Field ID (e.g., `customfield_12345`)
- Field name (e.g., `summary`, `description`, `assignee`)
- Field key (for system fields like `key`, `issuetype`, `status`)

#### acli jira workitem watcher

Work item watcher commands.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli jira workitem watcher list` | List watchers of an issue | `--json`, `--key string` |
| `acli jira workitem watcher remove` | Remove a watcher from an issue | `--key string`, `--user string` |

**Examples:**
```bash
acli jira workitem watcher list --key TEST-1
acli jira workitem watcher remove --key TEST-1 --user 5b10ac8d82e05b22cc7d4ef5
```

---

## Admin Commands

### acli admin

Admin commands for managing Atlassian organization.

| Command | Description |
|---------|-------------|
| `acli admin auth` | Authenticate to use Atlassian CLI for organization admin tasks |
| `acli admin user` | Manage a user within your Atlassian organization |

### acli admin auth

Authenticate to use Atlassian CLI for organization admin tasks.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli admin auth login` | Authenticate for the organization admin-specific tasks | `-e, --email string` (required), `--token` (read from stdin) |
| `acli admin auth logout` | Remove authentication and log out of organization admin account | None |
| `acli admin auth status` | Show status for organization admin account | None |
| `acli admin auth switch` | Switch between Atlassian organization admin accounts | `-o, --org string` |

**Examples:**
```bash
# Authenticate using API key
acli admin auth login --email admin@atlassian.com --token < token.txt
# Or
echo <token> | acli admin auth login --email admin@atlassian.com --token

# Switch accounts
acli admin auth switch --org myorgname
```

### acli admin user

Manage a user within your Atlassian organization.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli admin user activate` | Activate a user | `-e, --email string`, `-f, --from-file string`, `--id string`, `--ignore-errors`, `--json` |
| `acli admin user cancel-delete` | Cancel deletion of a managed account | `--email string`, `--from-file string`, `--id string`, `--ignore-errors`, `--json` |
| `acli admin user deactivate` | Deactivate a user | `-e, --email string`, `-f, --from-file string`, `--id string`, `--ignore-errors`, `--json` |
| `acli admin user delete` | Delete a managed account from Atlassian Administration | `--email string`, `--from-file string`, `--id string`, `--ignore-errors`, `--json` |

**Examples:**
```bash
# Activate users
acli admin user activate --email john@example.com,anna@example.com
acli admin user activate --id abcd,123
acli admin user activate --from-file listofmails.txt

# Delete managed account
acli admin user delete --email abc@atlassian.com
acli admin user delete --id 721217379117310973
```

---

## Rovo Dev Commands

### acli rovodev

Atlassian's AI coding agent: Rovo Dev (Beta).

| Command | Description |
|---------|-------------|
| `acli rovodev auth` | Authentication commands for Rovo Dev CLI |
| `acli rovodev run` | Run the Rovo Dev coding agent |
| `acli rovodev config` | Open the Rovo Dev configuration file in your editor |
| `acli rovodev log` | Open the Rovo Dev log file in your editor |
| `acli rovodev mcp` | Open the Rovo Dev MCP config file in your editor |
| `acli rovodev serve` | Run RovoDev CLI in server mode |

### acli rovodev auth

Authentication commands for Rovo Dev CLI.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli rovodev auth login` | Authenticate to use Rovo Dev specific tasks | `-e, --email string`, `--token` |
| `acli rovodev auth logout` | Remove authentication for a Rovo Dev account | None |
| `acli rovodev auth status` | Show status for Rovo Dev account | None |

**Examples:**
```bash
# Interactive mode
acli rovodev auth login

# Authenticate with email and token
acli rovodev auth login --email "user@atlassian.com" --token < token.txt
```

**Note:** Commands `run`, `config`, `log`, `mcp`, and `serve` require authentication first.

---

## Utility Commands

### acli completion

Generate the autocompletion script for the specified shell.

| Command | Description | Flags |
|---------|-------------|-------|
| `acli completion bash` | Generate the autocompletion script for bash | `--no-descriptions` |
| `acli completion fish` | Generate the autocompletion script for fish | `--no-descriptions` |
| `acli completion powershell` | Generate the autocompletion script for powershell | `--no-descriptions` |
| `acli completion zsh` | Generate the autocompletion script for zsh | `--no-descriptions` |

**Examples:**
```bash
# Load completions in current shell (bash/zsh)
source <(acli completion bash)
source <(acli completion zsh)

# Load completions in current shell (fish)
acli completion fish | source

# Load completions in current shell (powershell)
acli completion powershell | Out-String | Invoke-Expression
```

### acli feedback

Submit a request or report a problem.

**Flags:** `-a, --attachments strings`, `-d, --details string`, `-e, --email string`, `-s, --summary string`, `-t, --time string`

**Examples:**
```bash
acli feedback --summary "I have a problem" --details "I have a problem with the acli" --email "user@atlassian.com"
```

### acli help

Help provides help for any command in the application.

**Usage:** `acli help [command]`

**Examples:**
```bash
acli help
acli help jira
acli help jira workitem create
```

---

## Global Flags

All commands support:
- `-h, --help` - Show help for command
- `-v, --version` - Show version for acli

---

## Notes

- Most commands support `--json` flag for JSON output
- Many commands support `--csv` flag for CSV output
- Pagination is available for list/search commands via `--paginate` flag
- File input is supported via `--from-file` or `--from-json` flags in many commands
- Error handling can be controlled with `--ignore-errors` flag in bulk operations
- Interactive prompts can be skipped with `--yes` flag in destructive operations

---

*Generated from ACLI help output - Last updated: November 14, 2025*

