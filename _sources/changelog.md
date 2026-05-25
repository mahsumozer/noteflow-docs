# Changelog

## v0.1.0 — 2026-05-24

Initial release.

### Tools added

- **Notes (6):** `noteflow_notes_list`, `noteflow_notes_get`, `noteflow_notes_create`, `noteflow_notes_update`, `noteflow_notes_delete`, `noteflow_notes_search`
- **Projects (4):** `noteflow_projects_list`, `noteflow_projects_get`, `noteflow_projects_create`, `noteflow_projects_update`
- **Folders (3):** `noteflow_folders_list`, `noteflow_folders_get`, `noteflow_folders_create`
- **Tags (2):** `noteflow_tags_list`, `noteflow_tags_notes`
- **Tasks (3):** `noteflow_tasks_list`, `noteflow_tasks_create`, `noteflow_tasks_move`
- **AI (2):** `noteflow_ai_summarize`, `noteflow_ai_search_semantic`
- **Calendar (3):** `noteflow_calendar_list_notes`, `noteflow_calendar_get_entries`, `noteflow_calendar_add_entry`
- **Voice (2):** `noteflow_voice_list`, `noteflow_voice_get_transcript`

### Infrastructure

- Firebase Admin SDK authentication via service account JSON
- 13 feature flags for granular tool access control
- stdio transport (Claude Desktop, Cursor, VS Code)
- TypeScript source with declaration files
