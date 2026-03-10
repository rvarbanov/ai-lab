# Fields to Filter Out - Quick Review List

## ✅ Safe to Filter Out

### Top-Level Null Fields (10)
- changelog, editmeta, fieldsToInclude, names, operations, properties, renderedFields, schema, transitions, versionedRepresentations

### Empty Arrays (9) - BUT KEEP attachment
- components, customfield_12100, customfield_12403, customfield_12500, fixVersions, labels, subtasks, versions
- **Note**: Keep `attachment` even if empty - you need to know when attachments exist vs when they don't

### Null Standard Fields (7)
- aggregatetimeestimate, aggregatetimeoriginalestimate, duedate, environment, resolution, resolutiondate, security, timeestimate, timeoriginalestimate

### Null Custom Fields (~100+)
All customfield_* entries that are null (too many to list - they add significant bloat)

### Verbose Metadata (Consider Simplifying)
- **User objects**: accountId, accountType, active, avatarUrls (all 4 sizes), self, timeZone
  - **Keep**: displayName, emailAddress
- **System objects**: self URLs, iconUrl, avatarUrls (keep: id, name, key)
- **Top-level**: expand (metadata string)
- **Calculated**: workratio (-1)

## ✅ Fields to Keep

### Core (Essential)
- key, id, summary, description
- status (id, name), issuetype (id, name), priority (id, name)
- assignee, reporter, creator (displayName, emailAddress only)
- created, updated, resolutiondate

### Time Tracking
- timespent, aggregatetimespent, timetracking, progress

### Relationships
- parent (key, summary), issuelinks, subtasks

### Content
- **attachment** - MUST KEEP (even if empty) - to know when attachments exist
- comment (body, author displayName, created)
- worklog (timeSpent, author displayName, started)

### Custom Fields (with values)
- customfield_10000, customfield_10005, customfield_10007, customfield_10009, customfield_10012
- customfield_11306, customfield_11900, customfield_12000, customfield_12451, customfield_12470
- customfield_12594, customfield_12595

## 📝 Recommended Filtered Commands

### Option 1: Navigable Fields (Recommended)
Gets all fields that can be displayed in JIRA navigator - excludes most null/empty fields:
```bash
acli jira workitem view ERM-11175 --fields "*navigable" --json
```

### Option 2: Essential Fields Only (INCLUDES attachment)
```bash
acli jira workitem view ERM-11175 --fields "key,summary,status,issuetype,priority,assignee,reporter,created,updated,description,attachment,comment,parent,issuelinks,timespent,progress" --json
```

### Option 3: Essential + Custom Fields (INCLUDES attachment)
```bash
acli jira workitem view ERM-11175 --fields "key,summary,status,issuetype,priority,assignee,reporter,created,updated,description,attachment,comment,parent,issuelinks,timespent,progress,customfield_10007,customfield_10009,customfield_12594,customfield_12595" --json
```

### Option 4: Post-Process to Remove Nulls (BUT KEEP attachment)
Get all fields, then filter out nulls and empty arrays (but preserve attachment):
```bash
acli jira workitem view ERM-11175 --fields "*all" --json | jq 'walk(if type == "object" then with_entries(select(.value != null and (.key == "attachment" or .value != []))) else . end)'
```

## 🎯 Final Recommendation

**Use Option 2 or 3** - Since `*navigable` doesn't include `attachment`, you need to explicitly specify fields including `attachment` to ensure you can see when attachments exist.

### Recommended Command (Includes attachment):
```bash
acli jira workitem view ERM-11175 --fields "*navigable,attachment" --json
```

Or if you want more control:
```bash
acli jira workitem view ERM-11175 --fields "key,summary,status,issuetype,priority,assignee,reporter,created,updated,description,attachment,comment,parent,issuelinks,timespent,progress" --json
```

