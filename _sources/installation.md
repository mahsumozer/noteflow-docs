# Installation

## Prerequisites

| Requirement | Version |
|---|---|
| Node.js | 18 or later |
| npm | 9 or later |
| Firebase project | Noteflow app already set up |

---

## Install from source

Clone the Noteflow repository and install dependencies for the MCP server package:

```bash
git clone https://github.com/mahsumozer/noteflow.git
cd noteflow/packages/mcp-server
npm install
npm run build
```

The compiled server is now at `packages/mcp-server/dist/index.js`.

---

## Verify the installation

Run the server with `--help` to confirm everything is working:

```bash
node packages/mcp-server/dist/index.js --help
```

Expected output:

```
Options:
  --user-email      Firebase user email
  --project-id      Firebase project ID
  --key-path        Path to service account JSON
  --features        Comma-separated feature flags  [default: "notes:read"]
  --all-features    Enable all feature flags
  --max-page-size   Max results per page  [default: 100]
  --log-level       debug|info|warn|error  [default: "info"]
  --help            Show help
```

---

## Development mode

During development you can run the server with hot reload using `tsx`:

```bash
cd packages/mcp-server
npm run dev -- --user-email you@example.com --key-path ~/sa.json --all-features
```

---

## Next step

Follow the [Authentication](authentication.md) guide to create a Firebase service account key.
