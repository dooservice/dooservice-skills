# Working without touching production

Everything here needs the "Read and run" level and runs as a job: follow it with `follow_job`.

| Tool | Does |
| --- | --- |
| `clone_environment` | a copy of any environment, production included; `temporary` (the default) deletes itself after a day and stays on the source's branch, with data neutralized |
| `deploy_branch` | the latest commit of a branch in a development environment, after a backup; the environment follows that branch from then on |
| `rebuild_environment` | rebuild from its branch; `renew_image` also moves it to the platform's current Odoo image |
| `start_environment`, `stop_environment` | start or stop a development environment |
| `sync_submodules` | check its submodules out as its branch declares them |
| `create_backup` | a full backup of any environment, production included |
| `remove_environment` | delete a temporary copy you cloned, and no other |

## Rules

- Reproduce a production problem on a temporary clone of production, never on production.
- Clone from `backup_id` when the problem is in data production had at a known time.
- Deploy a branch to a copy to try it; the copy's own branch changes, production's does not.
- Expect at most five jobs at once for the organization's agents (`mcp_too_many_jobs`); wait for one to finish.
- Expect the server to hold few copies at once: clone one, finish with it, delete it.
