# Organization, project, and engine metadata

Source index: [Cloud system tables](https://docs.dremio.com/dremio-cloud/sql/system-tables/).
These runtime system tables are read-only. Querying them requires `ADMIN` or
`SELECT` on the specific runtime system table.

| Object | Scope and purpose | Source |
| --- | --- | --- |
| `sys.organization.projects` | Metadata for projects in an organization. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/projects/) |
| `sys.project.engines` | Metadata for engines in a project. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/engines/) |

```sql
SELECT project_id, project_name, state
FROM sys.organization.projects;
```

```sql
SELECT engine_id, engine_name, state
FROM sys.project.engines;
```

`sys.organization.projects` is organization-scoped; `sys.project.engines` is
project-scoped. Do not generalize either namespace to another Dremio platform.
