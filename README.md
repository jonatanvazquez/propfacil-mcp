<!-- mcp-name: io.github.jonatanvazquez/propfacil -->

<p align="center">
  <img src="assets/propfacil-icon-512.png" width="144" height="144" alt="PropFácil">
</p>

# PropFácil MCP

[![Validate distribution](https://github.com/jonatanvazquez/propfacil-mcp/actions/workflows/validate.yml/badge.svg)](https://github.com/jonatanvazquez/propfacil-mcp/actions/workflows/validate.yml)

Remote Model Context Protocol server for finding authorized real-estate listings in Mexico.
It provides public property search, details and contact options, plus OAuth-protected favorites
and publishing tools.

> [Leer en español](README.es.md)

## Connect

- **MCP endpoint:** `https://www.propfacil.com/api/mcp`
- **Transport:** Streamable HTTP
- **Current version:** `1.3.9`
- **Server card:** `https://www.propfacil.com/.well-known/mcp/server-card.json`
- **Documentation:** `https://www.propfacil.com/docs`

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

This is a hosted server. Do not clone this repository to run it locally and do not request an API key.
Clients that support MCP OAuth start the account-linking flow automatically when a protected tool is used.

See [installation instructions](docs/installation.md) for ChatGPT, Codex, Cline and generic clients.

## Capabilities

| Capability | Authentication |
|---|---|
| Search authorized listings by city, price, bedrooms, transaction type or radius | Public |
| Open a property record | Public |
| Retrieve authorized phone, WhatsApp or original-listing links for one property | Public |
| Render cards, comparison and map in MCP Apps-compatible hosts | Public |
| List and inspect favorite lists | OAuth |
| Save, rename, remove from or delete favorite lists | OAuth |
| View and publish the linked user's listings | OAuth |

The server exposes twelve model-visible tools plus one private UI restoration tool. See the complete
[tool reference](docs/tools.md) and [authentication details](docs/authentication.md).

## Host compatibility

All MCP clients can consume the tools and structured results when they support remote Streamable HTTP.
The interactive cards and map require a host with MCP Apps UI support; clients without that UI still
receive normal structured data. Protected tools additionally require a client that supports MCP OAuth.

## Distribution

This repository contains public distribution metadata, installation instructions and brand assets for
the hosted PropFácil MCP server. The production backend is maintained separately.

- Official MCP Registry metadata: [`server.json`](server.json)
- Official MCP Registry status: [`io.github.jonatanvazquez/propfacil` 1.3.9](https://registry.modelcontextprotocol.io/v0.1/servers?search=io.github.jonatanvazquez%2Fpropfacil)
- Smithery listing: [`jonatan/propfacil`](https://smithery.ai/servers/jonatan/propfacil)
- GitHub release: [`v1.3.9`](https://github.com/jonatanvazquez/propfacil-mcp/releases/tag/v1.3.9)
- Generic client configuration: [`.mcp.json`](.mcp.json)
- Agent-readable installer guidance: [`llms-install.md`](llms-install.md)
- Reusable directory listing fields: [`directory-profile.json`](directory-profile.json)
- Launch runbook: [`docs/launch-runbook.md`](docs/launch-runbook.md)
- Directory-specific notes: [`docs/directory-submissions.md`](docs/directory-submissions.md)
- Cline Marketplace submission: [issue #2287](https://github.com/cline/mcp-marketplace/issues/2287)

## Policies and support

- [Privacy policy](https://www.propfacil.com/privacidad)
- [Terms of service](https://www.propfacil.com/terminos)
- [Support](https://www.propfacil.com/soporte)
- [Security policy](SECURITY.md)

Metadata, configuration examples and documentation are available under the [MIT License](LICENSE).
The PropFácil name and logo are excluded from that license; see [TRADEMARKS.md](TRADEMARKS.md).
