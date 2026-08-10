# Jobs, usage, and ingest metadata

Source index: [Enterprise system tables](https://docs.dremio.com/current/reference/sql/system-tables/).
System tables are read-only: users cannot modify or drop them. For a system
table that supports delegated access, administrators use `GRANT` and `REVOKE`;
the three ADMIN-only exceptions are identified below.

For a delegable system table, use the current [GRANT/REVOKE syntax](https://docs.dremio.com/current/reference/sql/commands/rbac/):

```sql
GRANT SELECT ON TABLE <sys.table> TO { USER | ROLE } <principal>;
REVOKE SELECT ON TABLE <sys.table> FROM { USER | ROLE } <principal>;
```

Neutral delegated-access example:

```sql
GRANT SELECT ON TABLE sys.jobs TO USER <principal>;
```

| Object | Published purpose and access | Source |
| --- | --- | --- |
| `sys.jobs` | Jobs currently running in the Dremio instance. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/jobs/) |
| `sys.jobs_recent` | Jobs run during the number of prior days set by `jobs.max.age_in_days`. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/jobs_recent/) |
| `sys.history.model_usage` | AI model usage recorded by Dremio AI Features. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/model-usage/) |
| `sys.copy_errors_history` | Rejected CSV, JSON, or Parquet records from qualifying `COPY INTO` operations with `ON_ERROR 'continue'` or `ON_ERROR 'skip_file'`. `ADMIN` only, but results are still limited to COPY operations initiated by the querying user; do not infer cluster-wide history from `ADMIN`. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/copy-errors-history/) |
| `sys.copy_file_history` | Per-file history for `COPY INTO`, including autoingest-pipe loads. `ADMIN` only. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/copy-file-history/) |
| `sys.pipe_summary` | High-level historical statistics for autoingest pipes. `ADMIN` only. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/pipe_summary/) |

```sql
SELECT job_id, status, submitted_ts
FROM sys.jobs_recent;
```

Do not replace these Enterprise object names with another platform namespace.
