# mcp-data-nola

DataNewOrleans MCP — New Orleans open data (data.nola.gov, Socrata SODA API).

Part of [Pipeworx](https://pipeworx.io) — an MCP gateway connecting AI agents to 1476+ live data sources.

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

### What this endpoint actually serves

`tools/list` at `https://gateway.pipeworx.io/data-nola/mcp` returns the tools in the table
above **plus the shared Pipeworx meta-tools** — `ask_pipeworx`,
`discover_tools`, `search_within`, `remember`/`recall` and the rest of the
gateway-wide set. So the tool count you see is larger than this table: a
single-pack endpoint currently lists roughly 30 shared tools alongside the
pack's own. The connection's `initialize` response states its exact scope, and
is the authoritative answer for a given day.

This is deliberate, not multiplexing by accident. The meta-tools are what let a
scoped connection answer a question this pack does not cover — via
`ask_pipeworx`, which routes across the whole catalog — without you adding a
second MCP server. There is currently no way to mount a pack endpoint without
them; if the extra schemas cost you more context than the routing is worth,
connect to the full gateway once rather than to several pack endpoints.

Or connect to the full Pipeworx gateway to get every pack's tools listed
directly, instead of just this one's:

```json
{
  "mcpServers": {
    "pipeworx": {
      "url": "https://gateway.pipeworx.io/mcp"
    }
  }
}
```

Both URLs reach the same gateway and the same 1476+ data sources. The
only difference is which pack's tools are listed **directly**; `ask_pipeworx`
reaches all of them from either one.

## Using with ask_pipeworx

Instead of calling tools directly, you can ask questions in plain English —
this works on the pack endpoint above as well as on the full gateway:

```
ask_pipeworx({ question: "your question about Data Nola data" })
```

The gateway picks the right tool and fills the arguments automatically.

## More

- [Docs and guides](https://pipeworx.io/docs)
- [pipeworx.io](https://pipeworx.io)

## License

MIT
