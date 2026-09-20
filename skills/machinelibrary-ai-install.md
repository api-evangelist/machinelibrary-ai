# Machine Library MCP — Installation Guide

You are reading this because a user asked you to install the Machine Library MCP server.
Machine Library provides semantic search across millions of academic papers, books, Wikipedia, patents, Reddit, Telegram, and YouTube.

Machine Library is the search and AI product by Space Frontiers Company. Your existing account, API keys, and `spacefrontiers_*` tool names continue to work. The original `https://mcp.spacefrontiers.org` endpoint remains supported.

Follow these steps to set up the MCP connection.

## Step 1: Install with OAuth

For Claude Code, install at user scope and let the browser complete OAuth:

```bash
claude mcp add --transport http --scope user spacefrontiers https://mcp.machinelibrary.ai
```

`--scope user` makes the MCP available across all your projects. Drop it if you want it local to the current project only.

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
    "spacefrontiers": {
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
  `spacefrontiers_top_up_balance` MCP tool (fixed USD packages; the tool
  returns a standard MPP payment challenge to settle with Stripe)
- Review account and subscription options at https://machinelibrary.ai/profile

## Step 4: Verify

After installation, tell the user to restart their client, then try a search to verify.
Example: "Search for papers about quantum computing"

## Available Tools

- **spacefrontiers_search_documents** — compact search over papers, books, patents, standards, Wikipedia, and YouTube transcripts
- **spacefrontiers_search_social** — compact search over Reddit, Telegram, and Discord
- **spacefrontiers_fetch_document** — retrieve bounded full text and references by canonical URI
- **spacefrontiers_top_up_balance** — fund the account balance through a Stripe MPP payment challenge
- **spacefrontiers_search_in_document** — retrieve up to five matching passages within a document
