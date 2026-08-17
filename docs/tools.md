# Tool reference

## Public tools

| Tool | Purpose |
|---|---|
| `search_properties` | Search authorized inventory by city, transaction, price, bedrooms or radius |
| `get_property` | Retrieve one property record using an ID returned by search |
| `get_property_contact` | Retrieve authorized contact and destination links for one selected property |
| `render_property_results` | Render selected results in MCP Apps-compatible hosts |

## OAuth-protected tools

| Tool | Scope | Purpose |
|---|---|---|
| `my_listings` | `properties:read` | List publications owned by the linked user |
| `publish_property` | `properties:write` | Publish a user-confirmed property idempotently |
| `list_property_lists` | `lists:read` | List favorite lists owned by the linked user |
| `get_property_list` | `lists:read` | Read one owned list and its active entries |
| `save_property_to_list` | `lists:write` | Save a property, creating `Favoritos` when needed |
| `rename_property_list` | `lists:write` | Rename an owned favorite list |
| `remove_property_from_list` | `lists:write` | Remove one property while preserving the list |
| `delete_property_list` | `lists:write` | Permanently delete an owned list after confirmation |

Every tool declares an input schema, output schema, security scheme and safety annotations. Search never
filters inventory by its internal source field. Contact data is returned only for one specifically selected
property and the server does not provide bulk contact export.
