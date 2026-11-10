---
name: dooservice
description: >-
  Work on Odoo projects hosted on Dooservice through its MCP server
  (mcp.dooservice.sh): read environments, logs, deployments and backups, explain
  failures with explain_failure, clone production into temporary copies, deploy
  branches, read Odoo data with odoo_search_read, change code in a workspace and
  publish it as a pull request, and propose restores, rollbacks or rebuilds of
  production for an admin to approve. Use whenever a task names Dooservice, one
  of its projects or environments, or one of these tools.
---

# Working on Dooservice

Dooservice runs Odoo for consultancies: each project has production and development
environments on the customer's own server. You reach it only through its MCP tools, as
the person who connected you, with their role and the projects and level they granted.
Production is never changed by you: you clone it, work on the copy, and propose what only
a person may do.

| Task | Read |
| --- | --- |
| Connect, or understand a refusal about your connection | `connecting.md` |
| Find projects and environments; read logs, deployments, backups, jobs | `reading.md` |
| Something failed: a deployment, a module update, Odoo itself | `failures.md` |
| Try something without touching production: clone, deploy a branch, rebuild | `working.md` |
| Change the project's code and open a pull request | `code.md` |
| Read or change records in an environment's Odoo | `odoo-data.md` |
| Restore, roll back or rebuild production | `production.md` |

## Rules that hold everywhere

- Start every task with `list_projects`, then `list_environments`: ids come from there, never from guesses.
- Read the `mode` of an environment before acting on it; `production` is read only for you.
- Follow every job you start with `follow_job` until its state is `completed` or `failed`; a tool that starts a job returns before the work is done.
- Read a refusal's code, the text before the colon: it says what to do next, and the reason after it is meant for the person.
- Delete every temporary copy you cloned with `remove_environment` once you are done, and close every workspace with `workspace_close`.
- Tell the person what you changed, where, and what is waiting for them: a pull request to merge, a proposal to approve.
