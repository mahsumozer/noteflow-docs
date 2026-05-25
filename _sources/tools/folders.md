# Folders

Folders organize notes within a project. They support nesting via `parentId`.

**Required flag:** `folders:read` (read tools) · `folders:write` (write tools)

---

## noteflow_folders_list

List folders, optionally filtered by project.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `projectId` | string | No | Filter by project ID |

### Example response

```json
{
  "folders": [
    {
      "id": "folder_abc",
      "name": "Research",
      "projectId": "proj_xyz",
      "parentId": null,
      "color": "#FBBF24",
      "icon": "📂",
      "order": 1,
      "updatedAt": "2026-05-18T08:00:00.000Z"
    }
  ],
  "count": 1
}
```

---

## noteflow_folders_get

Get a single folder by ID.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | **Yes** | Folder ID |

---

## noteflow_folders_create

Create a new folder.

**Required flag:** `folders:write`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `name` | string | **Yes** | — | Folder name (max 200 chars) |
| `projectId` | string\|null | No | `null` | Parent project |
| `parentId` | string\|null | No | `null` | Parent folder (for nesting) |
| `color` | string | No | `#FBBF24` | Hex color |
| `icon` | string | No | `📂` | Emoji icon |
