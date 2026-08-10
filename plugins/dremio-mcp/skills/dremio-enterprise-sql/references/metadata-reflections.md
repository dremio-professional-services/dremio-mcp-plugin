# Reflection metadata

Source index: [Enterprise system tables](https://docs.dremio.com/current/reference/sql/system-tables/).
These system tables are read-only. The index says administrators use `GRANT`
and `REVOKE` for system tables that support delegated access.

For a delegable system table, use the current [GRANT/REVOKE syntax](https://docs.dremio.com/current/reference/sql/commands/rbac/):

```sql
GRANT SELECT ON TABLE <sys.table> TO { USER | ROLE } <principal>;
REVOKE SELECT ON TABLE <sys.table> FROM { USER | ROLE } <principal>;
```

| Object | Published purpose | Source |
| --- | --- | --- |
| `sys.reflections` | Reflection metadata in the Dremio instance. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/reflections/) |
| `sys.reflection_dependencies` | Runtime graph of Reflection dependencies. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/reflection-dependencies/) |
| `sys.materializations` | Monitoring history for Reflection materialization jobs. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/materializations/) |
| `sys.history.autonomous_reflections` | Historical metadata for Autonomous Reflections. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/autonomous-reflections-historical/) |
| `sys.results_cache` | Cached query-result metadata. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/results-cache/) |

```sql
SELECT reflection_id, reflection_name
FROM sys.reflections;
```
