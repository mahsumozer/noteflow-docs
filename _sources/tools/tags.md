# Tags

Tags in Noteflow are stored as string arrays on each note — there is no separate tag collection. The MCP server aggregates them from all notes on the fly.

**Required flag:** `tags:read`

---

## noteflow_tags_list

List all tags used across active notes, with their occurrence counts.

**Annotations:** `readOnlyHint`

### Parameters

None.

### Example response

```json
{
  "tags": [
    { "name": "meeting", "count": 23 },
    { "name": "work", "count": 18 },
    { "name": "ideas", "count": 12 },
    { "name": "q3", "count": 7 }
  ],
  "count": 4
}
```

Tags are sorted by count descending.

---

## noteflow_tags_notes

List notes that carry a specific tag.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `tag` | string | **Yes** | — | Exact tag name (case-sensitive) |
| `limit` | integer | No | `50` | Max results |

### Example response

```json
{
  "notes": [
    {
      "id": "note_abc",
      "type": "text",
      "title": "Q3 planning session",
      "tags": ["meeting", "q3", "planning"],
      "updatedAt": "2026-05-15T10:00:00.000Z"
    }
  ],
  "count": 1
}
```

---

## Adding and removing tags

Tags are managed through the **Notes** tools:

```json
// Add a tag
{
  "tool": "noteflow_notes_update",
  "id": "note_abc",
  "tags": ["meeting", "q3", "planning", "new-tag"]
}

// Remove a tag — just omit it from the array
{
  "tool": "noteflow_notes_update",
  "id": "note_abc",
  "tags": ["meeting", "q3"]
}
```
