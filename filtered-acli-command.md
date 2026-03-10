# Filtered ACLI Command - Final Recommendation

## ✅ Verified Working Command

This command includes all navigable fields PLUS the `attachment` field (which is required to know when attachments exist):

```bash
acli jira workitem view ERM-11175 --fields "*navigable,attachment" --json
```

### What This Command Does:
- ✅ Gets all navigable fields (fields that can be displayed in JIRA navigator)
- ✅ **Explicitly includes `attachment`** - so you can see when attachments exist vs when the array is empty
- ✅ Excludes most null fields and empty arrays automatically
- ✅ Returns JSON format for easy processing

### Test Results:
- ✅ Command works correctly
- ✅ `attachment` field is included (shows `[]` when empty, will show attachment objects when present)
- ✅ Significantly smaller payload than `*all` (navigable fields exclude most null/empty fields)

## Alternative: Explicit Field List

If you want more control over exactly which fields are returned:

```bash
acli jira workitem view ERM-11175 --fields "key,summary,status,issuetype,priority,assignee,reporter,created,updated,description,attachment,comment,parent,issuelinks,timespent,progress" --json
```

## Attachment Field Behavior

- **When empty**: `"attachment": []`
- **When attachments exist**: `"attachment": [{id, filename, size, created, author, ...}]`

This allows you to check `fields.attachment.length > 0` to determine if there are attachments to review.

## Summary

**Use this command:**
```bash
acli jira workitem view ERM-11175 --fields "*navigable,attachment" --json
```

This gives you:
- All useful navigable fields
- The `attachment` field (required for your review process)
- Minimal null/empty field bloat
- Clean, processable JSON output




