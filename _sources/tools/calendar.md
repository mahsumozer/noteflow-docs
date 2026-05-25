# Calendar

Calendar notes (`type: calendar`) contain a list of entries — each entry is either a note or a scheduled event, with optional recurrence and reminders.

**Required flag:** `calendar:read` (read tools) · `calendar:write` (write tools)

---

## noteflow_calendar_list_notes

List all calendar-type notes, optionally filtered by project.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `projectId` | string | No | Filter by project |

### Example response

```json
{
  "notes": [
    {
      "id": "note_cal1",
      "title": "Personal Calendar",
      "projectId": null,
      "entryCount": 14,
      "updatedAt": "2026-05-22T08:00:00.000Z"
    }
  ],
  "count": 1
}
```

---

## noteflow_calendar_get_entries

Get all entries from a calendar note, with optional date range filtering.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `noteId` | string | **Yes** | Calendar note ID |
| `from` | string | No | Start date `YYYY-MM-DD` (inclusive) |
| `to` | string | No | End date `YYYY-MM-DD` (inclusive) |

### Example response

```json
{
  "entries": [
    {
      "id": "entry_abc",
      "date": "2026-05-26",
      "kind": "event",
      "title": "Team standup",
      "text": "Daily sync with the engineering team.",
      "allDay": false,
      "startTime": "09:00",
      "endTime": "09:15",
      "recurrence": "daily",
      "reminder": "5m",
      "color": "#6366f1",
      "createdAt": "2026-05-01T10:00:00.000Z",
      "updatedAt": "2026-05-01T10:00:00.000Z"
    }
  ],
  "count": 1
}
```

---

## noteflow_calendar_add_entry

Add a new entry to a calendar note.

**Required flag:** `calendar:write`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `noteId` | string | **Yes** | — | Calendar note ID |
| `title` | string | **Yes** | — | Entry title |
| `date` | string | **Yes** | — | Date in `YYYY-MM-DD` format |
| `kind` | string | No | `note` | `note` or `event` |
| `text` | string | No | `""` | Entry body text |
| `allDay` | boolean | No | `true` | All-day entry |
| `startTime` | string | No | — | Start time `HH:MM` (ignored if `allDay`) |
| `endTime` | string | No | — | End time `HH:MM` |
| `recurrence` | string | No | `none` | `none`, `daily`, `weekly`, `monthly`, `yearly` |
| `reminder` | string | No | `none` | `none`, `at_time`, `5m`, `10m`, `30m`, `1h`, `1d` |
| `color` | string | No | `#6366f1` | Hex color |

### Example

```json
{
  "noteId": "note_cal1",
  "title": "Project review",
  "date": "2026-06-01",
  "kind": "event",
  "allDay": false,
  "startTime": "14:00",
  "endTime": "15:00",
  "reminder": "30m",
  "color": "#f59e0b"
}
```
