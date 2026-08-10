# Jobs, usage, and event metadata

Source index: [Cloud system tables](https://docs.dremio.com/dremio-cloud/sql/system-tables/).
System tables are read-only: users cannot modify or drop them. Historical system
tables require the `ADMIN` role. Runtime system tables require `ADMIN` or
`SELECT` on the specific system table.

## Project jobs and history

| Object | Purpose and constraint | Source |
| --- | --- | --- |
| `sys.project.jobs` | Jobs executing when queried; use history for completed-job metadata. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/jobs/) |
| `sys.project.history.jobs` | Historical project jobs; Dremio refreshes it once per hour, so records can appear later. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/jobs-historical/) |
| `sys.project.copy_errors_history` | Rejected records from qualifying `COPY INTO` operations; returns only operations initiated by the querying user. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/copy-errors-history/) |
| `sys.project.history.events` | Historical events in the project; Dremio refreshes it once per hour. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/events-historical/) |

```sql
SELECT job_id, status, submitted_ts
FROM sys.project.history.jobs;
```

## Organization model usage

| Object | Purpose | Source |
| --- | --- | --- |
| `sys.organization.history.model_usage` | Historical metadata for AI model usage at the organization level. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/model-usage/) |

```sql
SELECT model_provider_name, model_name
FROM sys.organization.history.model_usage;
```

Do not substitute an organization namespace for a project namespace, or vice
versa. These system-table scopes are part of the published object names.
