# Enterprise SQL platform boundaries

Use these current SQL-visible Enterprise distinctions to avoid importing Cloud
syntax or availability claims. Each row links directly to current public SQL
documentation.

| Enterprise distinction | SQL guidance | Source |
| --- | --- | --- |
| System metadata namespace | Enterprise system tables use the read-only `sys.*` namespace. The system-table index identifies `sys.copy_errors_history`, `sys.copy_file_history`, and `sys.pipe_summary` as ADMIN-only; separately, the current GRANT/REVOKE page says `sys.privileges` is viewable only by administrators. Treat these as documented constraints, not an inferred exhaustive access matrix. | [System tables](https://docs.dremio.com/current/reference/sql/system-tables/), [GRANT/REVOKE](https://docs.dremio.com/current/reference/sql/commands/rbac/) |
| Queue and tag routing | `SET QUEUE` and `RESET QUEUE` control queue routing; `SET TAG` and `RESET TAG` control session routing tags. | [SET QUEUE](https://docs.dremio.com/current/reference/sql/commands/set-queue/), [SET TAG](https://docs.dremio.com/current/reference/sql/commands/set-tag/) |
| Nessie versioning | Current SQL exposes Nessie branch, tag, merge, log, and version-context commands under the Nessie command index. | [Nessie commands](https://docs.dremio.com/current/reference/sql/commands/nessie/) |
| Reflections | `ALTER DATASET`, `ALTER TABLE`, and `ALTER VIEW` provide Reflection lifecycle and routing forms. | [Acceleration commands](https://docs.dremio.com/current/reference/sql/commands/acceleration/) |
| Autoingest pipes | `CREATE PIPE`, `ALTER PIPE`, `DESCRIBE PIPE`, and `DROP PIPE` are current Enterprise SQL commands. | [CREATE PIPE](https://docs.dremio.com/current/reference/sql/commands/create-pipe/) |
| Security objects and policies | Current RBAC SQL includes users, roles, object privileges, and UDF-backed row-access and column-masking policies. | [RBAC](https://docs.dremio.com/current/reference/sql/commands/rbac/), [row-access and column-masking policies](https://docs.dremio.com/current/reference/sql/commands/row-column-policies/) |

Do not translate these Enterprise names or commands to a different Dremio
platform. If a current public SQL page does not establish availability, state
that boundary instead of inferring it.
