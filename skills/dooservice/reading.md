# Reading

## Tools

| Tool | Answers |
| --- | --- |
| `list_projects` | the projects you were granted, with their Odoo version |
| `list_environments` | a project's environments: `id`, `mode`, `branch`, `commit`, `state`, `domain`, `custom_domain` |
| `describe_environment` | one environment whole: workers, timezone, language, automatic backups |
| `read_logs` | the last lines of Odoo's log, at most 2000 |
| `list_deployments` | deployments newest first: commits before and after, branch, status, who and when |
| `list_backups` | backups newest first; never a download, which only a person does on the panel |
| `follow_job` | a job's state, stage, progress and error |

## Rules

- Treat `stale: true` as the last state the server reported, not the present one; say so when it matters.
- Use `domain` as the address an environment answers at; `custom_domain` is its own domain and its check.
- Ask `read_logs` for the fewest lines that answer the question: 200 before 2000.
- Do not ask for a backup's file or a credential: no tool gives them, by design.
