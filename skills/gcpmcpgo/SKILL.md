---
name: gcpmcpgo
description: Install and configure Google Cloud managed remote MCP servers (BigQuery, Cloud Run, GKE, Compute Engine, Network Intelligence Center, Cloud SQL, Pub/Sub, and 30+ others) into Claude Code with OAuth. Use this skill when the user wants to add, set up, connect, or list GCP / Google Cloud MCP servers.
---

# gcpmcpgo — GCP Managed MCP Server Installer

Guides the user through registering a Google Cloud managed MCP server with Claude Code at **user scope** using OAuth.

## When to use

- User says "install the GCP/BigQuery/Cloud Run/… MCP server"
- User asks "which GCP MCP servers are available?"
- User wants to connect Claude Code to a Google Cloud API via MCP

## Workflow

### Step 1 — List supported servers

Read `references/gcp-mcp-servers.md` (located alongside this SKILL.md) and present the table to the user.

If the user names a product that is **not** in the table, fetch the live list from <https://docs.cloud.google.com/mcp/supported-products> and use that instead.

### Step 2 — Select a server

Ask the user which server they want to install. From their choice, determine:

- **Server name** — use the `Suggested Server Name` column (e.g. `GCP-BigQuery`). The user may override this.
- **Endpoint URL** — from the `MCP Endpoint` column. If it contains `REGION`, ask the user for a GCP region (e.g. `us-central1`) and substitute it.

### Step 3 — Gather OAuth credentials

Ask the user for their **OAuth Client ID** and **Client Secret**.

If they don't have one, show this guidance:

> 1. Open <https://console.cloud.google.com/apis/credentials> in your GCP project.
> 2. Click **+ Create Credentials → OAuth client ID**.
> 3. If prompted, configure the OAuth consent screen first (Internal or External).
> 4. Application type: **Web application**.
> 5. Under **Authorized redirect URIs**, add: `http://localhost:8089/callback`
> 6. Click **Create**, then copy the **Client ID** and **Client Secret**.

### Step 4 — Run the install command

Construct and execute via Bash (substitute the four placeholders):

```bash
claude mcp add --transport http \
  --client-id <CLIENT_ID> \
  --client-secret <CLIENT_SECRET> \
  --callback-port 8089 \
  --scope user \
  <SERVER_NAME> <ENDPOINT_URL>
```

Show the exact command to the user before running so they can confirm. Never log the client secret in plain summaries afterward.

### Step 5 — Authenticate

After the command succeeds, tell the user:

> Run `/mcp` in Claude Code, select **<SERVER_NAME>**, and complete the Google OAuth flow in the browser. Once it reports *Connected*, the server's tools are available.

## Reference

- Server catalog: `references/gcp-mcp-servers.md`
- Official docs: <https://docs.cloud.google.com/mcp/supported-products>
