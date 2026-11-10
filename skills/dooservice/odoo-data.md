# Odoo data

You read an environment's Odoo through its ORM, as its admin user. Every read is rolled
back on the server, whatever it did.

| Tool | Does |
| --- | --- |
| `odoo_models` | the models installed, filtered by `search` |
| `odoo_fields` | a model's fields: type, label, relation, required, stored, read only |
| `odoo_search_read` | how many records a `domain` matches and a page of them, at most 500 |
| `odoo_call` | a public method of a model or of `ids`, kept; development only, "Read and run" level |

## Rules

- Call `odoo_fields` before `odoo_search_read` on a model you have not read: field names change between Odoo versions.
- Ask for the `fields` you need and the smallest `limit` that answers; page with `offset`.
- Write domains as lists: `[["state", "=", "posted"], ["company_id", "=", 1]]`.
- Change data on a development copy with `odoo_call`, never by hand-made SQL: there is none.
- Expect production reads to need the console's production permission and the organization's leave for AI (`mcp_production_data_closed`).
