# Notes

Notes are the primary entity in Noteflow. Eight note types are supported: `text`, `canvas`, `voice`, `image`, `drawing`, `presentation`, `page`, and `calendar`.

**Required flag:** `notes:read` (read tools) · `notes:write` (write tools)

---

## noteflow_notes_list

List notes with optional filters. Returns metadata without full content.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `projectId` | string | No | — | Filter by project ID |
| `folderId` | string | No | — | Filter by folder ID |
| `tags` | string[] | No | — | Only notes that have **all** of these tags |
| `type` | string | No | — | One of `text`, `canvas`, `voice`, `image`, `drawing`, `presentation`, `page`, `calendar` |
| `archived` | boolean | No | `false` | Include archived notes |
| `starred` | boolean | No | — | Only starred notes |
| `trashed` | boolean | No | `false` | Show trashed notes instead of active |
| `limit` | integer | No | `50` | Max results (1–100) |
| `cursor` | string | No | — | Pagination cursor (ISO date from previous `updatedAt`) |

### Example response

```json
{
  "notes": [
    {
      "id": "abc123",
      "type": "text",
      "title": "Meeting notes — Q3 kickoff",
      "tags": ["meeting", "q3"],
      "color": "#ffffff",
      "icon": "📝",
      "starred": false,
      "archived": false,
      "pinned": true,
      "wordCount": 342,
      "projectId": "proj_xyz",
      "folderId": null,
      "createdAt": "2026-05-01T09:00:00.000Z",
      "updatedAt": "2026-05-10T14:22:00.000Z"
    }
  ],
  "count": 1
}
```

---

## noteflow_notes_get

Get a single note by ID including full content.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | **Yes** | Note ID |

### Example response

```json
{
  "id": "abc123",
  "type": "text",
  "title": "Meeting notes — Q3 kickoff",
  "content": {
    "html": "<p>Attendees: Alice, Bob...</p>",
    "plainText": "Attendees: Alice, Bob..."
  },
  "tags": ["meeting", "q3"],
  "aiSummary": "A kickoff meeting covering Q3 goals and team assignments.",
  "aiActionItems": ["Send agenda by Friday", "Book room for next session"],
  "createdAt": "2026-05-01T09:00:00.000Z",
  "updatedAt": "2026-05-10T14:22:00.000Z"
}
```

---

## noteflow_notes_create

Create a new note.

**Required flag:** `notes:write`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `type` | string | No | `text` | Note type |
| `title` | string | No | `""` | Note title |
| `content` | string | No | — | Plain text or HTML body (text notes only) |
| `projectId` | string\|null | No | `null` | Assign to a project |
| `folderId` | string\|null | No | `null` | Place inside a folder |
| `tags` | string[] | No | `[]` | Initial tags |
| `color` | string | No | `#ffffff` | Hex background color |
| `starred` | boolean | No | `false` | Mark as starred |

### Example

```json
{
  "type": "text",
  "title": "Weekly review",
  "content": "This week I worked on the MCP server integration.",
  "tags": ["weekly", "work"],
  "projectId": "proj_xyz"
}
```

### Response

```json
{ "id": "newNote456", "message": "Note created" }
```

---

## noteflow_notes_update

Update note metadata or content fields. Only the fields you provide are changed.

**Required flag:** `notes:write`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | **Yes** | Note ID |
| `title` | string | No | New title |
| `content` | string | No | New plain text / HTML body (text notes only) |
| `tags` | string[] | No | Replaces the entire tag list |
| `color` | string | No | Hex color |
| `starred` | boolean | No | Toggle star |
| `archived` | boolean | No | Toggle archive |
| `pinned` | boolean | No | Toggle pin |
| `folderId` | string\|null | No | Move to folder |
| `projectId` | string\|null | No | Move to project |

---

## noteflow_notes_delete

Move a note to trash. Set `permanent: true` to delete it forever.

**Required flag:** `notes:write` · **Annotations:** `destructiveHint`

```{warning}
Permanent deletion cannot be undone. Omit the `permanent` flag or set it to `false` to soft-delete (move to trash) instead.
```

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `id` | string | **Yes** | — | Note ID |
| `permanent` | boolean | No | `false` | Permanently delete instead of trash |

---

## noteflow_notes_search

Full-text keyword search across note titles, tags, and plain-text content.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `query` | string | **Yes** | — | Search query (case-insensitive) |
| `type` | string | No | — | Limit to a specific note type |
| `projectId` | string | No | — | Limit to a project |
| `limit` | integer | No | `20` | Max results |

### Searched fields

The query is matched against: note title, tags, plain text (`text` notes), text note (`voice`/`image`), transcript (`voice`), calendar entry titles and text, canvas text/sticky objects, presentation slide text, page HTML (stripped).
