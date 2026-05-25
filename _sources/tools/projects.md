# Projects

Projects group notes and folders together. Each project includes a Kanban task board with configurable columns and tasks.

**Required flag:** `projects:read` (read tools) · `projects:write` (write tools)

---

## noteflow_projects_list

List all projects.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `archived` | boolean | No | `false` | Include archived projects |

### Example response

```json
{
  "projects": [
    {
      "id": "proj_abc",
      "name": "MCP Integration",
      "description": "Building the Noteflow MCP server",
      "color": "#6366f1",
      "icon": "🔌",
      "archived": false,
      "noteCount": 12,
      "taskCount": 5,
      "updatedAt": "2026-05-20T10:00:00.000Z"
    }
  ],
  "count": 1
}
```

---

## noteflow_projects_get

Get a project by ID including the full task board (columns and tasks).

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | **Yes** | Project ID |

### Example response

```json
{
  "id": "proj_abc",
  "name": "MCP Integration",
  "taskBoard": {
    "columns": [
      { "id": "col_1", "title": "To-do", "color": "#6366f1", "order": 0 },
      { "id": "col_2", "title": "In progress", "color": "#f59e0b", "order": 1 },
      { "id": "col_3", "title": "Complete", "color": "#10b981", "order": 3 }
    ],
    "tasks": [
      {
        "id": "task_1",
        "columnId": "col_2",
        "title": "Write tool documentation",
        "priority": "high",
        "dueDate": "2026-05-25",
        "order": 0
      }
    ]
  }
}
```

---

## noteflow_projects_create

Create a new project. A default Kanban board with four columns (To-do, In progress, In review, Complete) is created automatically.

**Required flag:** `projects:write`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `name` | string | **Yes** | — | Project name (max 200 chars) |
| `description` | string | No | `""` | Project description |
| `color` | string | No | `#6366f1` | Hex accent color |
| `icon` | string | No | `📁` | Emoji icon |

---

## noteflow_projects_update

Update project metadata.

**Required flag:** `projects:write`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | **Yes** | Project ID |
| `name` | string | No | New name |
| `description` | string | No | New description |
| `color` | string | No | New hex color |
| `icon` | string | No | New emoji |
| `archived` | boolean | No | Archive or unarchive |
