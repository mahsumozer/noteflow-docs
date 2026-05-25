# Noteflow MCP Server

**Noteflow MCP** is a [Model Context Protocol](https://modelcontextprotocol.io) server that gives any MCP-compatible AI client — Claude Desktop, Cursor, VS Code Copilot, and others — direct, structured access to your Noteflow data.

Once configured, you can talk to your notes, projects, and tasks in natural language:

> *"Find all my notes tagged 'meeting' from last month and summarize the key action items."*
> *"Create a new project called 'Q3 Planning' and add three tasks."*
> *"Search my voice recordings for anything related to the API design."*

---

## What it provides

```{list-table}
:header-rows: 1
:widths: 20 15 65

* - Category
  - Tools
  - Description
* - **Notes**
  - 6
  - List, read, create, update, delete, and search all note types (text, canvas, voice, image, drawing, presentation, page, calendar)
* - **Projects**
  - 4
  - Browse and manage your Kanban-style project boards
* - **Folders**
  - 3
  - Navigate the folder hierarchy within projects
* - **Tags**
  - 2
  - Explore tags and find notes by tag
* - **Tasks**
  - 3
  - Read and manage tasks inside project boards
* - **AI**
  - 2
  - Fetch AI summaries and run semantic similarity search
* - **Calendar**
  - 3
  - Read and write calendar entries in calendar-type notes
* - **Voice**
  - 2
  - Access voice note transcripts and metadata
```

**Total: 25 tools** — all selectively enabled via feature flags.

---

## How it works

```
MCP Client (Claude Desktop / Cursor / VS Code)
        ↕  stdio / JSON-RPC
  Noteflow MCP Server  (packages/mcp-server)
        ↕  Firebase Admin SDK
       Google Firestore
```

The server runs as a local process on your machine. It authenticates to Firebase using a **service account key** you download once from the Firebase Console. Your data never passes through a third-party relay — it goes directly from Firestore to your AI client.

---

## Quick start

1. [Install](installation.md) the MCP server
2. [Set up authentication](authentication.md) with a Firebase service account
3. Add the server to your [MCP client config](configuration.md)
4. Start chatting with your notes

---

## Open source

Both the Noteflow application and this MCP server are open source. The MCP server lives in the `packages/mcp-server/` directory of the main repository.
