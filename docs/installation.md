# Installation

PropFácil runs as a hosted MCP server. Every client connects to the same production endpoint:

```text
https://www.propfacil.com/api/mcp
```

No package installation or API key is required.

## ChatGPT and Codex

When PropFácil is available in the public plugin directory, install it from that directory. During
development, enable developer mode, create an MCP connection using the production endpoint above and
select **Streamable HTTP**. Account linking starts only when a protected tool is used.

## Generic MCP clients

Clients that use an `mcpServers` JSON object commonly accept:

```json
{
  "mcpServers": {
    "propfacil": {
      "type": "http",
      "url": "https://www.propfacil.com/api/mcp"
    }
  }
}
```

Some clients call the transport `streamable-http`, `streamableHttp` or simply `http`. Use the
client's Streamable HTTP option and the exact endpoint URL.

## Cline

For Cline remote-server settings, use:

```json
{
  "mcpServers": {
    "propfacil": {
      "type": "streamableHttp",
      "url": "https://www.propfacil.com/api/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Keep `autoApprove` empty. Search and detail calls are safe reads, but publishing and list mutations
should remain visible to the user.

## What to expect

- Public tools work without signing in.
- Favorites and publishing trigger OAuth in compatible clients.
- MCP Apps-compatible hosts show interactive property cards and maps.
- Other clients receive the same property data as structured MCP results without the custom UI.

If the client cannot connect, verify that it supports remote Streamable HTTP and allows OAuth discovery.
See [authentication](authentication.md) for the discovery endpoints.
