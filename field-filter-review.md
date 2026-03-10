# Field Filter Review - ERM-11175

This document lists fields that can be filtered out from JIRA work item responses to reduce payload size and focus on essential information.

## Summary

- **Total fields analyzed**: ~200+ fields
- **Null fields**: ~120 fields
- **Empty arrays**: 9 fields
- **Verbose metadata**: Multiple nested objects

## 1. Top-Level Null Fields (Can be excluded)

These top-level fields are always null and can be safely excluded:

- `changelog` - null
- `editmeta` - null
- `fieldsToInclude` - null
- `names` - null
- `operations` - null
- `properties` - null
- `renderedFields` - null
- `schema` - null
- `transitions` - null
- `versionedRepresentations` - null

**Recommendation**: Exclude all of these.

## 2. Empty Arrays (Can be excluded)

These fields contain empty arrays and can be excluded:

- `fields.attachment` - []
- `fields.components` - []
- `fields.customfield_12100` - []
- `fields.customfield_12403` - []
- `fields.customfield_12500` - []
- `fields.fixVersions` - []
- `fields.labels` - []
- `fields.subtasks` - []
- `fields.versions` - []

**Recommendation**: Exclude all of these unless you need to know when they're empty.

## 3. Null Fields in fields Object (Can be excluded)

These fields are null in this work item (may have values in other items):

### Time Tracking (null)
- `fields.aggregatetimeestimate` - null
- `fields.aggregatetimeoriginalestimate` - null

### Standard Fields (null)
- `fields.duedate` - null
- `fields.environment` - null
- `fields.resolution` - null
- `fields.resolutiondate` - null
- `fields.security` - null
- `fields.timeestimate` - null
- `fields.timeoriginalestimate` - null

### Custom Fields (null) - ~100+ fields
All custom fields with null values (customfield_10001 through customfield_12807, many are null)

**Recommendation**: 
- Exclude null standard fields (duedate, environment, resolution, etc.) unless needed
- Exclude null custom fields - too many to list individually, but they add significant bloat
- Note: Some custom fields may have values in other work items, so this is context-dependent

## 4. Verbose Metadata Fields (Consider simplifying)

### Top-Level Metadata
- `expand` - Long string listing expanded resources (metadata)
- `self` - API URL (useful for API calls, but not for display)

### User Object Verbosity
User objects (assignee, creator, reporter, comment authors, etc.) contain:
- `accountId` - Internal ID (usually not needed for display)
- `accountType` - "atlassian" or "app" (usually not needed)
- `active` - boolean (usually not needed)
- `avatarUrls` - Object with 4 different size URLs (16x16, 24x24, 32x32, 48x48)
- `self` - API URL
- `timeZone` - User timezone

**Keep**: `displayName`, `emailAddress`

**Recommendation**: If possible, simplify user objects to just displayName and emailAddress.

### Calculated/System Fields
- `fields.workratio` - -1 (calculated field, often not useful)

### Nested Object Metadata
- `self` URLs throughout (in issuetype, priority, status, project, etc.)
- `iconUrl` in various objects
- `avatarUrls` in project objects

**Recommendation**: Keep essential IDs and names, exclude URLs and icons unless needed for display.

## 5. Fields to KEEP (Essential Information)

### Core Identification
- `id` - Work item ID
- `key` - Work item key (e.g., ERM-11175)
- `self` - API URL (useful for API operations)

### Essential Fields
- `fields.summary` - Title
- `fields.description` - Description
- `fields.status` - Current status (simplified: id, name)
- `fields.issuetype` - Issue type (simplified: id, name)
- `fields.priority` - Priority (simplified: id, name)
- `fields.project` - Project (simplified: id, key, name)
- `fields.assignee` - Assignee (simplified: displayName, emailAddress)
- `fields.reporter` - Reporter (simplified: displayName, emailAddress)
- `fields.creator` - Creator (simplified: displayName, emailAddress)
- `fields.created` - Creation date
- `fields.updated` - Last update date
- `fields.resolutiondate` - Resolution date (if not null)

### Time Tracking (if not null)
- `fields.timespent` - Time spent
- `fields.aggregatetimespent` - Aggregate time spent
- `fields.timetracking` - Time tracking object
- `fields.progress` - Progress percentage

### Relationships
- `fields.parent` - Parent issue (simplified: key, summary)
- `fields.issuelinks` - Linked issues (simplified: key, type, summary)
- `fields.subtasks` - Subtasks (if not empty)

### Content
- `fields.comment` - Comments (simplified: body text, author displayName, created)
- `fields.worklog` - Work logs (simplified: timeSpent, author displayName, started)

### Custom Fields (with values)
- `fields.customfield_10000` - Last viewed date
- `fields.customfield_10005` - Some numeric value
- `fields.customfield_10007` - Sprints
- `fields.customfield_10009` - Parent key
- `fields.customfield_10012` - Some value
- `fields.customfield_11306` - User field (simplified)
- `fields.customfield_11900` - Pull request info
- `fields.customfield_12000` - Team/component
- `fields.customfield_12451` - Priority/severity
- `fields.customfield_12470` - Some option
- `fields.customfield_12594` - Product
- `fields.customfield_12595` - Module

**Note**: Custom field IDs vary by JIRA instance. The ones listed here are specific to this instance.

## 6. Recommended Filtered Command

Based on this analysis, here are recommended field sets:

### Minimal Set (Core Information Only)
```bash
acli jira workitem view ERM-11175 --fields "key,summary,status,issuetype,priority,assignee,reporter,created,updated,description" --json
```

### Standard Set (Most Common Use Cases)
```bash
acli jira workitem view ERM-11175 --fields "key,summary,status,issuetype,priority,assignee,reporter,creator,created,updated,description,comment,parent,issuelinks,timespent,progress,customfield_10007,customfield_10009,customfield_12594,customfield_12595" --json
```

### Custom Set (Exclude null/empty, keep populated)
Since acli doesn't support excluding fields directly, you would need to:
1. Use `*navigable` to get navigable fields
2. Post-process JSON to remove nulls/empty arrays
3. Or specify exact fields you want

**Note**: The `--fields` flag doesn't support exclusion patterns for nested objects or automatic null filtering. You'll need to specify exactly which fields you want.

## 7. Post-Processing Recommendation

Since acli doesn't support advanced filtering, consider:

1. **Use `*navigable` fields** - Gets fields that can be displayed in JIRA navigator
   ```bash
   acli jira workitem view ERM-11175 --fields "*navigable" --json
   ```

2. **Post-process JSON** - Use jq or Python to filter out nulls and empty arrays
   ```bash
   acli jira workitem view ERM-11175 --fields "*all" --json | jq 'walk(if type == "object" then with_entries(select(.value != null and .value != [])) else . end)'
   ```

3. **Specify exact fields** - List only the fields you need (most reliable)

## Next Steps

1. Review this list and identify which fields are actually needed for your use case
2. Test the recommended commands
3. Create a final filtered command based on your specific requirements

