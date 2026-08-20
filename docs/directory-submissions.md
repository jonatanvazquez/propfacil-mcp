# Directory publication

This repository is the public distribution source for the hosted PropFácil MCP server.
Use the complete [launch runbook](launch-runbook.md) for go/no-go, release order, verification,
monitoring and rollback. This page is the compact directory-specific reference.

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
3. Create and push the unique semantic version tag `v1.3.8`.
4. Verify the published record through the Registry API.

GitHub OIDC is used for namespace verification, so no registry token is stored as a secret.

Published on **20 August 2026** as version `1.3.8`; the Registry reports status `active` and
`isLatest: true`. Release tag: [`v1.3.8`](https://github.com/jonatanvazquez/propfacil-mcp/releases/tag/v1.3.8).

## Smithery

Publish the existing URL rather than uploading or rebuilding the server:

```sh
smithery mcp publish "https://www.propfacil.com/api/mcp" -n @jonatanvazquez/propfacil
```

Smithery can scan the public tools without OAuth. If a scan requires static metadata, use the existing
server card at `/.well-known/mcp/server-card.json`.

Current status: CLI 4.11.1 publish flow prepared. Account authentication must be completed by the
owner before the URL can be published.

## Glama

Glama ingests Official MCP Registry records. After registry publication, search for PropFácil and claim
the resulting listing. PropFácil is a hosted connector: use the remote endpoint and do not configure
Glama to build the private backend from this metadata-only repository.

## MCP.so

Select **Remote Server** and use endpoint `https://www.propfacil.com/api/mcp` with name `PropFácil`.
The current route advertises a USD 39 one-time paid submission, so payment and submission require a
separate explicit approval.

## PulseMCP

Manual submissions are temporarily paused. PulseMCP recommends the Official MCP Registry and says it
will ingest entries from there automatically. Recheck the intake after the official release is visible.

## Cline Marketplace

Use `assets/propfacil-icon-400.png`, this repository URL and [`llms-install.md`](../llms-install.md). The
installation target is the remote Streamable HTTP endpoint; it does not require cloning or a local command.
The issue template requires truthful confirmation that Cline completed setup from the public instructions;
use the prepared [issue draft](submission-drafts/cline-marketplace.md) only after that test passes.

Completed on 20 August 2026 with Cline CLI 3.0.55. The server installed as `streamableHttp` without
warnings, and the submission is tracked in
[cline/mcp-marketplace#2287](https://github.com/cline/mcp-marketplace/issues/2287).
