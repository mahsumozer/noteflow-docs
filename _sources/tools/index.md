# Tool Reference

The Noteflow MCP server exposes **25 tools** organized into 8 categories. Each tool maps to a Firestore operation on your Noteflow data.

---

## Tool naming convention

All tools follow the pattern `noteflow_{category}_{action}`:

- `noteflow_notes_list` — list notes
- `noteflow_projects_get` — get a single project
- `noteflow_tasks_create` — create a task

---

## Tool annotations

Each tool is annotated with hints that tell the AI client how to use it safely:

| Annotation | Meaning |
|---|---|
| `readOnlyHint: true` | The tool does not modify any data |
| `destructiveHint: true` | The tool may permanently delete data |

---

## Categories

```{list-table}
:header-rows: 1
:widths: 20 10 70

* - Category
  - Count
  - What you can do
* - [Notes](notes.md)
  - 6
  - Full CRUD on all note types plus keyword search
* - [Projects](projects.md)
  - 4
  - Browse and manage project boards
* - [Folders](folders.md)
  - 3
  - Navigate folder hierarchy
* - [Tags](tags.md)
  - 2
  - Explore and filter by tags
* - [Tasks](tasks.md)
  - 3
  - Read and write Kanban tasks
* - [AI](ai.md)
  - 2
  - Summaries and semantic search
* - [Calendar](calendar.md)
  - 3
  - Read and add calendar entries
* - [Voice](voice.md)
  - 2
  - Access transcripts of voice recordings
```
