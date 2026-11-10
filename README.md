# Dooservice skills

An [agent skill](https://agentskills.io) that teaches AI agents (Claude Code, Cursor,
Codex, OpenCode…) to work on Odoo projects hosted on [Dooservice](https://dooservice.sh)
through its MCP server, the way the platform means them to: read first, change only copies,
publish code as pull requests, and leave production to people.

```sh
npx skills add dooservice/dooservice-skills
claude mcp add --transport http dooservice https://mcp.dooservice.sh/mcp
```

## What it covers

| Guide | For |
| --- | --- |
| `connecting.md` | the MCP server, the three levels and the refusals about a connection |
| `reading.md` | projects, environments, logs, deployments, backups and jobs |
| `failures.md` | `explain_failure` and how to find the cause of a failure |
| `working.md` | clones, branches, rebuilds and backups outside production |
| `code.md` | workspaces, pull request rules and trying a branch on a copy |
| `odoo-data.md` | reading and changing records through the ORM |
| `production.md` | proposals an admin approves |

For Odoo itself — its framework and its apps, version by version — add
[odoo-skills](https://github.com/dooservice/odoo-skills) too.

## License

LGPL-3.0-only, as odoo-skills.
