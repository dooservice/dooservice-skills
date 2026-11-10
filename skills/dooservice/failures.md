# Explaining a failure

Call `explain_failure` with the project and the environment, and `job_id` when you know
the job. It answers in one call with:

- `job`: the failed job, its `kind`, `stage`, `error` and `error_code`;
- `deployment`: the last deployment and, when it failed, `since_last_working`, the commits it brought since the last one that worked;
- `log.errors`: the error lines of Odoo's log, each with three lines around it and every traceback whole; `log.last`: the last lines as they are.

## Rules

- Read the last line of a traceback first: it names the exception and the file.
- Match the failure to a commit in `since_last_working` before guessing a cause.
- Fix it in a workspace and try it on a copy (`code.md`, `working.md`); never retry the failed deployment unchanged.
- Stop after three attempts that fail the same way, and tell the person what you tried and what you found.
