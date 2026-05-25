# Configuration

## Environment variables

All CLI options have an environment variable equivalent:

| Variable | CLI flag | Description |
|---|---|---|
| `NOTEFLOW_USER_EMAIL` | `--user-email` | Firebase user email (**required**) |
| `NOTEFLOW_FIREBASE_PROJECT_ID` | `--project-id` | Firebase project ID (default: `not-alma-uygulamasi-b72a8`) |
| `NOTEFLOW_SERVICE_ACCOUNT_KEY_PATH` | `--key-path` | Path to service account JSON |
| `NOTEFLOW_SERVICE_ACCOUNT_KEY_JSON` | — | Inline JSON string (alternative to path) |
| `NOTEFLOW_FEATURES` | `--features` | Comma-separated feature flags (default: `notes:read`) |
| `NOTEFLOW_MAX_PAGE_SIZE` | `--max-page-size` | Max results per paginated request (default: `100`) |
| `NOTEFLOW_LOG_LEVEL` | `--log-level` | `debug`, `info`, `warn`, `error` (default: `info`) |

---

## Claude Desktop

Add to `~/Library/Application Support/Claude/claude_desktop_config.json` (macOS) or `%APPDATA%\Claude\claude_desktop_config.json` (Windows):

### Read-only

```json
{
  "mcpServers": {
    "noteflow": {
      "command": "node",
      "args": ["/absolute/path/to/noteflow/packages/mcp-server/dist/index.js"],
      "env": {
        "NOTEFLOW_USER_EMAIL": "your@email.com",
        "NOTEFLOW_SERVICE_ACCOUNT_KEY_PATH": "/home/user/.config/noteflow/service-account.json",
        "NOTEFLOW_FEATURES": "notes:read,projects:read,tags:read,ai,voice:read"
      }
    }
  }
}
```

### Full access

```json
{
  "mcpServers": {
    "noteflow": {
      "command": "node",
      "args": ["/absolute/path/to/noteflow/packages/mcp-server/dist/index.js"],
      "env": {
        "NOTEFLOW_USER_EMAIL": "your@email.com",
        "NOTEFLOW_SERVICE_ACCOUNT_KEY_PATH": "/home/user/.config/noteflow/service-account.json",
        "NOTEFLOW_FEATURES": "notes:read,notes:write,projects:read,projects:write,folders:read,folders:write,tags:read,tasks:read,tasks:write,ai,calendar:read,calendar:write,voice:read"
      }
    }
  }
}
```

After editing the file, restart Claude Desktop.

---

## Cursor

Add to `.cursor/mcp.json` in your home directory or project:

```json
{
  "mcpServers": {
    "noteflow": {
      "command": "node",
      "args": ["/path/to/noteflow/packages/mcp-server/dist/index.js"],
      "env": {
        "NOTEFLOW_USER_EMAIL": "your@email.com",
        "NOTEFLOW_SERVICE_ACCOUNT_KEY_PATH": "/home/user/.config/noteflow/service-account.json",
        "NOTEFLOW_FEATURES": "notes:read,notes:write,ai"
      }
    }
  }
}
```

---

## VS Code (GitHub Copilot)

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "noteflow": {
      "type": "stdio",
      "command": "node",
      "args": ["/path/to/noteflow/packages/mcp-server/dist/index.js"],
      "env": {
        "NOTEFLOW_USER_EMAIL": "your@email.com",
        "NOTEFLOW_SERVICE_ACCOUNT_KEY_PATH": "/home/user/.config/noteflow/service-account.json",
        "NOTEFLOW_FEATURES": "notes:read,ai"
      }
    }
  }
}
```

---

## Using npx (without cloning)

Once published to npm, the server can be run without cloning the repository:

```json
{
  "mcpServers": {
    "noteflow": {
      "command": "npx",
      "args": ["-y", "noteflow-mcp"],
      "env": {
        "NOTEFLOW_USER_EMAIL": "your@email.com",
        "NOTEFLOW_SERVICE_ACCOUNT_KEY_PATH": "/home/user/.config/noteflow/service-account.json"
      }
    }
  }
}
```

---

## Verifying the connection

After adding the server to your MCP client, ask the AI:

> *"List my Noteflow tools"*

or

> *"Show me my last 5 notes in Noteflow"*

If everything is configured correctly, the AI will call `noteflow_notes_list` and return your notes.
