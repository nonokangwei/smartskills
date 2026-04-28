# gcpmcpgo

An [agent skill](https://agentskills.io/) that walks you through installing any **Google Cloud managed MCP server** (BigQuery, Cloud Run, GKE, Compute Engine, Network Intelligence Center, Cloud SQL, Pub/Sub, Spanner, and 30+ more) into **Claude Code** with OAuth.

## Install

```bash
npx skills add nonokangwei/smartskills -a claude-code
```

Or install globally for all projects:

```bash
npx skills add nonokangwei/smartskills -a claude-code -g
```

## Usage

Inside Claude Code, either invoke the skill directly:

```
/gcpmcpgo
```

…or just ask naturally:

```
set up the GCP BigQuery MCP server
```

The skill will:

1. Show you the catalog of supported GCP MCP servers
2. Ask which one you want
3. Guide you through creating an OAuth Client ID in the GCP Console
4. Run `claude mcp add --transport http …` with the correct endpoint
5. Prompt you to complete the OAuth flow via `/mcp`

## Supported servers

See [`skills/gcpmcpgo/references/gcp-mcp-servers.md`](skills/gcpmcpgo/references/gcp-mcp-servers.md), sourced from the official [Google Cloud MCP supported products](https://docs.cloud.google.com/mcp/supported-products) page.

## License

MIT
