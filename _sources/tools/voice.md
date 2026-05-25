# Voice

Voice notes store an audio recording alongside its transcript text and an optional hand-written text note. The MCP server provides read access to the transcribed content.

**Required flag:** `voice:read`

```{note}
Recording new audio requires microphone access, which is a browser-only API. The MCP server only exposes transcripts of recordings already made in the Noteflow app.
```

---

## noteflow_voice_list

List voice notes with metadata and a short transcript snippet.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `projectId` | string | No | — | Filter by project |
| `limit` | integer | No | `50` | Max results |

### Example response

```json
{
  "notes": [
    {
      "id": "note_v1",
      "title": "Architecture brainstorm",
      "projectId": "proj_xyz",
      "duration": 183,
      "wordCount": 412,
      "transcriptSnippet": "So the main idea here is to decouple the data layer from the UI completely…",
      "updatedAt": "2026-05-19T16:00:00.000Z"
    }
  ],
  "count": 1
}
```

`duration` is in seconds.

---

## noteflow_voice_get_transcript

Get the full transcript and text note of a voice recording.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | **Yes** | Voice note ID |

### Example response

```json
{
  "id": "note_v1",
  "title": "Architecture brainstorm",
  "duration": 183,
  "wordCount": 412,
  "transcriptText": "So the main idea here is to decouple the data layer from the UI completely. If we do that, we can swap out Firebase for any backend without touching the components...",
  "textNote": "Key points: decouple data layer, use adapters, evaluate Supabase as alternative",
  "aiSummary": "A brainstorming session about decoupling the data layer using an adapter pattern.",
  "aiActionItems": ["Research Supabase adapter libraries", "Draft the data layer interface"],
  "updatedAt": "2026-05-19T16:00:00.000Z"
}
```

`transcriptText` is the auto-generated speech-to-text output. `textNote` is a hand-written supplement added in the app.
