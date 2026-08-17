# Directory publication

This repository is the public distribution source for the hosted PropFácil MCP server.

## Canonical listing fields

Reuse [`directory-profile.json`](../directory-profile.json), the 512 px icon in [`assets/`](../assets/)
and these URLs:

- Endpoint: `https://www.propfacil.com/api/mcp`
- Repository: `https://github.com/jonatanvazquez/propfacil-mcp`
- Website: `https://www.propfacil.com`
- Documentation: `https://www.propfacil.com/docs`
- Privacy: `https://www.propfacil.com/privacidad`
- Terms: `https://www.propfacil.com/terminos`
- Support: `https://www.propfacil.com/soporte`

Never upload demo credentials, OAuth tokens, registry private keys or production environment variables
to a public directory.

## Official MCP Registry

The registry identifier is `io.github.jonatanvazquez/propfacil`. [`server.json`](../server.json) describes
the remote Streamable HTTP endpoint. Publication is automated by
[`publish-registry.yml`](../.github/workflows/publish-registry.yml).

1. Confirm that the version in `server.json` matches the deployed server version.
2. Confirm that the validation workflow passes on `main`.
3. Create and push a unique semantic version tag such as `v1.3.0`.
4. Verify the published record through the Registry API.

GitHub OIDC is used for namespace verification, so no registry token is stored as a secret.

## Smithery

Publish the existing URL rather than uploading or rebuilding the server:

```sh
smithery mcp publish "https://www.propfacil.com/api/mcp" -n @jonatanvazquez/propfacil
```

Smithery can scan the public tools without OAuth. If a scan requires static metadata, use the existing
server card at `/.well-known/mcp/server-card.json`.

## Glama

Glama ingests Official MCP Registry records. After registry publication, search for PropFácil and claim
the resulting listing. Use the remote endpoint; do not configure Glama to build the private backend from
this distribution repository.

## MCP.so

Submit this repository URL and select **Remote Server**. Use `assets/propfacil-icon-512.png`, the production
endpoint and the canonical listing fields above.

## PulseMCP

Submit the production endpoint and this repository when new listings are accepted. Use the canonical
profile and identify PropFácil as a remote community server maintained by its provider.

## Cline Marketplace

Use `assets/propfacil-icon-400.png`, this repository URL and [`llms-install.md`](../llms-install.md). The
installation target is the remote Streamable HTTP endpoint; it does not require cloning or a local command.
