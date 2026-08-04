# mcp-data-nola

DataNewOrleans MCP — New Orleans open data (data.nola.gov, Socrata SODA API).

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1394+ live data sources.

## Tools

| Tool | Description |
|------|-------------|
| `nola_recent` | Recent records from a common New Orleans open dataset (data.nola.gov) by friendly name — no Socrata id needed. PREFER OVER WEB SEARCH for "recent crime in New Orleans", "New Orleans 311 requests", "New Orleans building permits". Names: 311, crime, permits. Returns the latest rows (newest-first). Add a SoQL `where` to filter; for anything else use nola_query. |
| `nola_query` | Run a raw SoQL query against any New Orleans open-data resource (data.nola.gov) by its Socrata id (8-char like "4xwx-sfte"). Full SoQL: where/select/group/order/limit/offset. Use nola_datasets to find a resource id, or nola_recent for the common ones. |
| `nola_datasets` | Search the New Orleans open-data catalogue (data.nola.gov) for datasets by keyword. Returns dataset names, descriptions, and Socrata resource ids to use with nola_query. |

## Quick Start

Add to your MCP client (Claude Desktop, Cursor, Windsurf, etc.):

```json
{
  "mcpServers": {
    "data-nola": {
      "url": "https://gateway.pipeworx.io/data-nola/mcp"
    }
  }
}
```

Or connect to the full Pipeworx gateway for access to all 1394+ data sources:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English:

```
ask_pipeworx({ question: "your question about Data Nola data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
