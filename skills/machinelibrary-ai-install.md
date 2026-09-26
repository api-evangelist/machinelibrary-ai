# Machine Library MCP — Installation Guide

You are reading this because a user asked you to install the Machine Library MCP server.
Machine Library provides semantic search across millions of academic papers, books, Wikipedia, patents, Reddit, Telegram, and YouTube.

Machine Library is the search and AI product by Space Frontiers Company. The server advertises `machinelibrary_*` tool names. Existing accounts, API keys, and legacy `spacefrontiers_*` tool calls continue to work. The original `https://mcp.spacefrontiers.org` endpoint remains supported.

Follow these steps to set up the MCP connection.

## Step 1: Install with OAuth

For Claude Code, install at user scope and let the browser complete OAuth:

```bash
claude mcp add --transport http --scope user machinelibrary https://mcp.machinelibrary.ai
```

`--scope user` makes the MCP available across all your projects. Drop it if you want it local to the current project only.

For Codex, use its built-in MCP OAuth flow:

```bash
codex mcp add machinelibrary --url https://mcp.machinelibrary.ai
```

If authorization did not start during setup, run:

```bash
codex mcp login machinelibrary --scopes search
```

Reuse an existing connection instead of adding a duplicate. The local server name
(`machinelibrary`) identifies the integration; the consent page identifies the
client (`Codex`). Its separate **Unverified application** notice describes the
client's verification status. Check the name and callback before approving.
See the [authentication guide](https://machinelibrary.ai/auth.md).

## Step 2: Other clients

### Claude Desktop

Open **Settings → Connectors → Add custom connector**, name it
**Machine Library**, enter `https://mcp.machinelibrary.ai`, then select
**Connect** and complete OAuth in the browser. Remote servers do not work when
added directly to `claude_desktop_config.json`.

### Cursor / Windsurf / other HTTP clients

Add this server to the client's MCP configuration. OAuth-capable clients will
open a browser automatically:

```json
{
  "mcpServers": {
    "machinelibrary": {
      "type": "http",
      "url": "https://mcp.machinelibrary.ai"
    }
  }
}
```

If the client does not support remote MCP OAuth, create a key at
https://machinelibrary.ai/keys and add
`"headers": {"Authorization": "Bearer YOUR_API_KEY"}` to the server object.

## Step 3: Add Credits

Tell the user:

- Review current usage rates and billing units on the [pricing page](https://machinelibrary.ai/pricing)
- Opt-in citation backlinks on a fetch add a separately billed search
- Add credits at https://machinelibrary.ai/payments
- Agents with a Stripe MPP-capable payment client can instead call the
  `machinelibrary_top_up_balance` MCP tool (fixed USD packages; the tool
  returns a standard MPP payment challenge to settle with Stripe)
- Review account and subscription options at https://machinelibrary.ai/profile

## Step 4: Verify

After installation, restart or reconnect the client to refresh its tool catalog, then try a search to verify. Existing connections may show cached `spacefrontiers_*` names until refreshed.
Example: "Search for papers about quantum computing"

## Available Tools

- **machinelibrary_search_documents** — compact search over papers, books, patents, standards, Wikipedia, and YouTube transcripts
- **machinelibrary_search_social** — compact search over Reddit, Telegram, and Discord
- **machinelibrary_fetch_document** — retrieve bounded full text and references by canonical URI
- **machinelibrary_top_up_balance** — fund the account balance through a Stripe MPP payment challenge
- **machinelibrary_search_in_document** — retrieve up to five matching passages within a document
- **machinelibrary_research** — generate a cited answer with optional conversation follow-ups; billed per turn
- **machinelibrary_search_feedback** — rate inspected results; generate a UUID for `feedback_id` and reuse it with the same payload on retries
