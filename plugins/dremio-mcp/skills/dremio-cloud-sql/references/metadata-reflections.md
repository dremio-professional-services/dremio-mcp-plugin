# Reflection metadata

Source index: [Cloud system tables](https://docs.dremio.com/dremio-cloud/sql/system-tables/).
All objects below are read-only. Historical tables require `ADMIN`; runtime
tables require `ADMIN` or `SELECT` on the specific runtime system table.

| Object | Purpose | Source |
| --- | --- | --- |
| `sys.project.reflections` | Metadata for Reflections in a project. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/reflections/) |
| `sys.project.reflection_dependencies` | Runtime dependency graph for Reflections in the current project. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/reflection-dependencies/) |
| `sys.project.materializations` | Monitoring history for Reflection materialization jobs. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/materializations/) |
| `sys.project.results_cache` | State of cached query results in a project; each row is one cache entry. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/results-cache/) |
| `sys.project.history.autonomous_reflections` | Historical metadata for Autonomous Reflections in a project. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/autonomous-reflections-historical/) |

```sql
SELECT reflection_id, reflection_name, status
FROM sys.project.reflections;
```

`sys.project.materializations` is categorized as historical by the public
system-table index even though its object name does not contain `history`.
