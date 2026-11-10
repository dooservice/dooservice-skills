# Connecting

The MCP server is `https://mcp.dooservice.sh/mcp`, over HTTP with OAuth. The person adds it
to their client (Claude Code: `claude mcp add --transport http dooservice https://mcp.dooservice.sh/mcp`),
signs in on the Dooservice panel, and picks one organization, its projects and a level.

## Levels

| Level | You may |
| --- | --- |
| Read only | read projects, environments, logs, deployments, backups, jobs and Odoo data where their role reads it |
| Read and run | also clone, deploy branches, rebuild, start, stop, back up, sync submodules, call Odoo methods and publish code, in development only |
| Propose on production | also ask an admin to restore, roll back or rebuild production |

Your effective permission is what the level grants and the person's role allows, both,
checked on every call: a role they lose, you lose at once.

## Refusals about the connection

- `mcp_level_required`: ask the person to connect you again with a higher level.
- `mcp_org_closed`: an owner or admin turned agents off for the organization; stop and say so.
- `mcp_odoo_unavailable`, `mcp_workspaces_unavailable`: the server's agent has not updated yet; say so and do the task another way.
- A `401` from the server: the connection was revoked or expired; the client signs in again.
