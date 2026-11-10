# Changing code

You change code in a workspace of your own on the server, apart from every environment,
and publish it as a pull request. Nothing reaches an environment until somebody merges it,
or until you deploy its branch to a copy.

## Flow

1. `workspace_open` on a development environment, usually a temporary clone of production; follow its job.
2. `workspace_files`, `workspace_read` to understand the code; `workspace_write` to write a file whole, or delete it.
3. `workspace_diff` to read everything you changed before publishing.
4. `workspace_publish` with a commit `message`, a pull request `title` and `body`; follow its job.
5. `deploy_branch` the workspace's `branch` to a copy and check it with `read_logs` or `explain_failure`.
6. `workspace_close` once done.

## Pull request rules

The server refuses a pull request that breaks them, and says which rule.

- Write the title as `[TAG] modules: summary`, at most 80 characters, without a final period.
- Use one tag: `FIX`, `IMP`, `ADD`, `REF`, `REM`, `MOV`, `REV`, `PERF`, `I18N`, `MIG`, `CLN`, `LINT`, `REL` or `MERGE`.
- Name the technical names of the modules touched, comma separated, in lowercase.
- Write the body with these `## ` sections in this order, every one filled but the last: Summary, Why, Changes, How to test, Deployment, Risks, References. The person's language may name them differently; the refusal lists the names it expects.
- Do not sign the body or add `Co-authored-by` lines: Dooservice signs it.

## Rules

- Write only inside the workspace: never `.git`, a symbolic link or a submodule, which is a repository of its own.
- Write each file whole, at most 256 KiB; read it first and keep what you do not mean to change.
- Publish again from the same workspace to update the same pull request.
