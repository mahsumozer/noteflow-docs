# Authentication

The Noteflow MCP server uses the **Firebase Admin SDK** to access Firestore directly. This requires a **service account key** — a JSON file that identifies the server to Firebase.

```{note}
The service account key grants full read/write access to your Firebase project. Store it securely and never commit it to version control.
```

---

## Step 1 — Download a service account key

1. Open the [Firebase Console](https://console.firebase.google.com) and select your Noteflow project.
2. Click the gear icon → **Project settings**.
3. Go to the **Service accounts** tab.
4. Click **Generate new private key** → **Generate key**.
5. A JSON file is downloaded — for example `not-alma-uygulamasi-b72a8-firebase-adminsdk-xxxx.json`.

---

## Step 2 — Store the key safely

Move the key to a location outside your project directory:

```bash
mkdir -p ~/.config/noteflow
mv ~/Downloads/not-alma-uygulamasi-*.json ~/.config/noteflow/service-account.json
chmod 600 ~/.config/noteflow/service-account.json
```

---

## Step 3 — Test the connection

```bash
node packages/mcp-server/dist/index.js \
  --user-email your@email.com \
  --key-path ~/.config/noteflow/service-account.json \
  --features notes:read \
  --log-level debug
```

You should see:

```
[noteflow-mcp] Starting for user your@email.com (uid: abc123...)
[noteflow-mcp] Enabled tools (3): noteflow_notes_list, noteflow_notes_get, noteflow_notes_search
```

If you see an error like `user-not-found`, double-check that `--user-email` matches the email you registered in Noteflow.

---

## Alternative: inline JSON (for CI / containers)

Instead of a file path, you can pass the key content as an environment variable:

```bash
export NOTEFLOW_SERVICE_ACCOUNT_KEY_JSON=$(cat ~/.config/noteflow/service-account.json)
node packages/mcp-server/dist/index.js --user-email your@email.com
```

This is useful for Docker deployments or CI pipelines where mounting files is inconvenient.

---

## Security notes

```{warning}
- The service account bypasses Firestore Security Rules — it has full database access.
- The feature flag system (see [Feature Flags](feature-flags.md)) is the only access boundary. Only enable the flags you need.
- Rotate the service account key periodically in the Firebase Console.
```
