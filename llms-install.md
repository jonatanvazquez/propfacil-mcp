# Install PropFácil MCP

PropFácil is a hosted remote MCP server. Do not clone, build or execute this repository.

## Connection

- Name: `propfacil`
- Transport: Streamable HTTP
- URL: `https://www.propfacil.com/api/mcp`

Use the client's native remote-MCP configuration. A common configuration shape is:

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

If the client distinguishes `http` from `streamable-http`, choose its Streamable HTTP option.
Do not configure an API key or static bearer token.

## Authentication behavior

Property search, details, contact lookup and result rendering are public. Favorites, lists and
publishing are protected by OAuth. When the user requests a protected operation, let the MCP client
start authorization discovery and open the PropFácil consent flow. Never ask the user to paste an
access token into chat or save credentials in the MCP configuration.

## Verification

After connecting, list the tools and confirm that `search_properties` is present. Test with:

`Search for properties for rent in Toluca and limit the result to five.`

Do not test write tools without explicit user intent. Deleting a favorite list is destructive and
requires confirmation.
