# Authentication

PropFácil uses OAuth 2.1-style authorization for user-owned data and write actions. Public catalog tools
remain available without authentication.

## Discovery

- Protected resource metadata: `https://www.propfacil.com/.well-known/oauth-protected-resource`
- Authorization server metadata: `https://www.propfacil.com/.well-known/oauth-authorization-server`
- Dynamic client registration: `https://www.propfacil.com/api/oauth/register`
- Authorization endpoint: `https://www.propfacil.com/oauth/authorize`
- Token endpoint: `https://www.propfacil.com/api/oauth/token`

The authorization flow uses Authorization Code with PKCE S256 and the MCP resource value
`https://www.propfacil.com/api/mcp`.

## Scopes

| Scope | Purpose |
|---|---|
| `properties:read` | View listings owned by the linked user |
| `properties:write` | Publish a listing for the linked user |
| `lists:read` | View the linked user's favorite lists |
| `lists:write` | Save, rename, remove from or delete favorite lists |

## Client guidance

Clients should initiate OAuth only after a protected tool returns an authorization challenge. Tokens
must be handled by the MCP host and must never be requested in chat, committed to a repository or placed
in a static MCP configuration file.
