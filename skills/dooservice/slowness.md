# Slowness

When someone says Odoo is slow, measure before you change anything.

## Measure

1. Call `explain_slowness` with the project and the environment.
2. Read `load` first:
   - `memory_mb` near `memory_limit_mb` means the instance is short of memory; say so and suggest more workers or a bigger server, never a code change.
   - `cpu_percent` near 100 per worker means the instance is busy; look at the statements.
   - `p95_response_ms` is the time 95 in 100 requests were answered within over the last hour; above 2000 is slow for people.
   - `server_errors_last_hour` above zero means requests fail; call `explain_failure` too.
3. Read `slow_statements`, heaviest first by `total_ms`:
   - A high `mean_ms` with few `calls` is one slow query: find the model and the domain in its text.
   - A low `mean_ms` with many `calls` is a query run in a loop: find the code that runs it once per record.
4. Read `scanned_tables`: each is a large table read whole more often than through an index.

If `statements_note` is set, the server has no statement statistics yet; say so and rely on `load` and `scanned_tables`.

## Fix

1. Clone production into a temporary copy with `clone_environment`.
2. Open a workspace on the copy's branch and change the code:
   - Add `index=True` to the field the slow query filters on, or a composite index in `init()` with `tools.create_index`.
   - Move a query out of a loop with `search_read` or `read_group` over all the records at once.
3. Publish the workspace as a pull request and deploy its branch to the copy.
4. Call `explain_slowness` on the copy and compare `mean_ms` and `p95_response_ms` before you say it is faster.

## Do not

- Do not change PostgreSQL settings or ask for them: the platform sizes them for the server.
- Do not add an index to production yourself: it reaches production through the pull request, merged by a person.
- Do not run heavy queries with `odoo_search_read` on production to investigate; read the copy.
