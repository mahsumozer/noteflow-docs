# Feature Flags

Feature flags let you control exactly which tools the MCP server exposes. Only the tools you enable appear in the AI client's tool list — keeping the context window lean and limiting write access to what you actually need.

---

## Available flags

```{list-table}
:header-rows: 1
:widths: 25 15 60

* - Flag
  - Access
  - Tools enabled
* - `notes:read`
  - Read
  - `noteflow_notes_list`, `noteflow_notes_get`, `noteflow_notes_search`
* - `notes:write`
  - Write
  - `noteflow_notes_create`, `noteflow_notes_update`, `noteflow_notes_delete`
* - `projects:read`
  - Read
  - `noteflow_projects_list`, `noteflow_projects_get`
* - `projects:write`
  - Write
  - `noteflow_projects_create`, `noteflow_projects_update`
* - `folders:read`
  - Read
  - `noteflow_folders_list`, `noteflow_folders_get`
* - `folders:write`
  - Write
  - `noteflow_folders_create`
* - `tags:read`
  - Read
  - `noteflow_tags_list`, `noteflow_tags_notes`
* - `tasks:read`
  - Read
  - `noteflow_tasks_list`
* - `tasks:write`
  - Write
  - `noteflow_tasks_create`, `noteflow_tasks_move`
* - `ai`
  - Read
  - `noteflow_ai_summarize`, `noteflow_ai_search_semantic`
* - `calendar:read`
  - Read
  - `noteflow_calendar_list_notes`, `noteflow_calendar_get_entries`
* - `calendar:write`
  - Write
  - `noteflow_calendar_add_entry`
* - `voice:read`
  - Read
  - `noteflow_voice_list`, `noteflow_voice_get_transcript`
```

---

## Setting flags

### Via environment variable

```bash
export NOTEFLOW_FEATURES="notes:read,notes:write,projects:read,tasks:read,ai"
```

### Via CLI argument

```bash
node dist/index.js --features "notes:read,notes:write,projects:read,ai"
```

### Enable everything

```bash
node dist/index.js --all-features
```

---

## Recommended profiles

### Read-only assistant
The safest configuration — the AI can answer questions about your notes but cannot change anything.

```
NOTEFLOW_FEATURES=notes:read,projects:read,folders:read,tags:read,tasks:read,ai,calendar:read,voice:read
```

### Full personal assistant
All read and write access. Suitable when you trust the AI client fully.

```
NOTEFLOW_FEATURES=notes:read,notes:write,projects:read,projects:write,folders:read,folders:write,tags:read,tasks:read,tasks:write,ai,calendar:read,calendar:write,voice:read
```

### Quick capture
Minimal — just enough to create and search notes.

```
NOTEFLOW_FEATURES=notes:read,notes:write
```

### Research mode
Read and search everything, including AI semantic search and voice transcripts.

```
NOTEFLOW_FEATURES=notes:read,tags:read,ai,voice:read,calendar:read
```

---

## Default

When no flags are specified, the server defaults to **`notes:read`** only — the safest possible baseline.
