# AI Tools

The AI tools expose the Noteflow app's built-in AI features: stored summaries and semantic similarity search.

**Required flag:** `ai`

---

## noteflow_ai_summarize

Return the AI-generated summary for a note. If the note has no stored summary, the tool extracts the first 500 characters of plain text as a fallback.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Description |
|---|---|---|---|
| `id` | string | **Yes** | Note ID |

### Example response

```json
{
  "id": "note_abc",
  "title": "Q3 kickoff meeting",
  "summary": "A kickoff meeting covering Q3 OKRs, team assignments, and the new product roadmap.",
  "aiTags": ["meeting", "okr", "roadmap"],
  "aiActionItems": [
    "Share meeting recording by EOD Friday",
    "Update JIRA tickets with new priorities"
  ],
  "hasAiSummary": true
}
```

When `hasAiSummary` is `false`, the summary is a plain-text extract — not AI generated.

---

## noteflow_ai_search_semantic

Search notes by semantic similarity using stored vector embeddings. Returns notes ranked by relevance score.

**Annotations:** `readOnlyHint`

### Parameters

| Parameter | Type | Required | Default | Description |
|---|---|---|---|---|
| `query` | string | **Yes** | — | Natural language search query |
| `limit` | integer | No | `10` | Max results |
| `threshold` | float | No | `0.15` | Minimum similarity score (0–1) |

### Example response

```json
{
  "results": [
    {
      "id": "note_abc",
      "type": "text",
      "title": "API design decisions",
      "score": 0.742,
      "method": "embedding"
    },
    {
      "id": "note_def",
      "type": "voice",
      "title": "Architecture brainstorm recording",
      "score": 0.631,
      "method": "embedding"
    }
  ],
  "embeddedNoteCount": 87
}
```

### How the embedding works

Noteflow uses a 128-dimensional local hash vector (no external AI API). Every word in the note is hashed into a position in a fixed-size vector, and the vector is L2-normalized. Cosine similarity is computed between the query vector and each stored note vector. This is the same algorithm the Noteflow web app uses for its semantic search feature, so scores are consistent between the app and the MCP server.

### Fallback behavior

If a note has no stored embedding (`embeddedNoteCount` is low), the tool falls back to keyword matching and returns results with `method: "keyword-fallback"`. To get embeddings for your notes, open them in the Noteflow app — embeddings are computed automatically when a note is opened or edited.
