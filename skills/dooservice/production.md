# Production

You never change production. With the "Propose on production" level you ask a person to:

| `action` | Needs | What runs once approved |
| --- | --- | --- |
| `restore` | `backup_id` | the backup restored, after a backup of production as it is |
| `rollback` | `revision` | production back to that deployment |
| `rebuild` | nothing | production rebuilt from its branch |

## Flow

1. `propose_production_action` with the project, the production environment, the `action` and a `reason`.
2. Tell the person the proposal waits for an admin of the project on the panel; the admins also get an email.
3. `get_proposal` until its `state` is `approved`, `rejected` or `expired` (a day).
4. Once approved, `follow_job` its `job_id`.

## Rules

- Write the `reason` for the admin who decides: what is wrong, what you checked, and why this action fixes it.
- Prove the action on a temporary copy first when you can, and say so in the reason.
- Do not propose the same action twice while one is pending.
- `create_backup` is the one change you make to production yourself: it changes nothing in it.
