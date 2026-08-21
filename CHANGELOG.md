# Changelog

All notable distribution metadata changes are documented here.

## 1.3.9 — 2026-08-21

- Added human-readable descriptions to every MCP input parameter for directory and ChatGPT scans.
- Completed Smithery listing metadata with the PropFácil description, homepage and production icon.
- Added an automated regression check so future tools cannot omit parameter descriptions.
- Kept the thirteen-tool surface, OAuth scopes and v13 MCP Apps resource stable.

## 1.3.8 — 2026-08-20

- Aligned Registry and directory metadata with the deployed MCP server version 1.3.8.
- Documented twelve model-visible tools plus the private UI restoration tool.
- Updated validation for the v13 MCP Apps resource and the thirteen-tool production surface.
- Documented current Official MCP Registry lifecycle states while retaining immutable version metadata.
- Published `io.github.jonatanvazquez/propfacil` 1.3.8 to the Official MCP Registry and opened the Cline Marketplace submission.
- Published the hosted endpoint to Smithery as `jonatan/propfacil`.

## 1.3.1 — 2026-08-18

- Added a go/no-go and launch runbook for the Official MCP Registry and downstream directories.
- Documented verification, monitoring, rollback and immutable Registry version handling.
- Hardened widget contact normalization for hosts that omit nullable fields.
- Versioned the property-results MCP Apps resource as v5 to avoid stale host caches.

## 1.3.0 — 2026-08-17

- Added public property search, detail and authorized contact tools.
- Added MCP Apps cards, detail, comparison and map UI.
- Added OAuth-protected listing publication and favorite-list CRUD.
- Added OpenAI-compatible tool annotations, output schemas and security schemes.
- Added public server card, production brand assets and directory metadata.
