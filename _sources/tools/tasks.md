# Tasks

Tasks belong to a project's Kanban board. They are stored inside the project document (not a separate collection), grouped into columns.

**Required flag:** `tasks:read` (read tools) · `tasks:write` (write tools)

---

## noteflow_tasks_list

List tasks in a project's board, optionally filtered by column or priority.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `projectId` | string | **Yes** | Project ID |
| `columnId` | string | No | Filter by column ID |
| `priority` | string | No | `low`, `medium`, or `high` |

### Example response

```json
{
  "columns": [
    { "id": "col_1", "title": "To-do", "color": "#6366f1", "order": 0 },
    { "id": "col_2", "title": "In progress", "color": "#f59e0b", "order": 1 }
  ],
  "tasks": [
    {
      "id": "task_abc",
      "columnId": "col_2",
      "columnTitle": "In progress",
      "title": "Write authentication docs",
      "description": "Cover service account setup and token rotation.",
      "priority": "high",
      "dueDate": "2026-05-25",
      "order": 0,
      "createdAt": "2026-05-18T09:00:00.000Z",
      "updatedAt": "2026-05-20T11:00:00.000Z"
    }
  ],
  "taskCount": 1
}
```

---

## noteflow_tasks_create

Create a new task in a project column.

**Required flag:** `tasks:write`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `projectId` | string | **Yes** | — | Project ID |
| `columnId` | string | **Yes** | — | Column ID (from `noteflow_projects_get`) |
| `title` | string | **Yes** | — | Task title |
| `description` | string | No | `""` | Task description |
| `priority` | string | No | `medium` | `low`, `medium`, or `high` |
| `dueDate` | string\|null | No | `null` | ISO date string e.g. `2026-06-01` |

### Tip

Use `noteflow_projects_get` first to retrieve the column IDs before creating tasks.

---

## noteflow_tasks_move

Move a task to a different column. This is the canonical way to mark a task as complete — move it to the "Complete" column.

**Required flag:** `tasks:write`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `projectId` | string | **Yes** | Project ID |
| `taskId` | string | **Yes** | Task ID |
| `targetColumnId` | string | **Yes** | Destination column ID |

### Completing a task

```json
{
  "tool": "noteflow_tasks_move",
  "projectId": "proj_abc",
  "taskId": "task_xyz",
  "targetColumnId": "col_complete"
}
```
