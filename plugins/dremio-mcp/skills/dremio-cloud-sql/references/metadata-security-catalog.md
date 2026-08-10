# Security and catalog metadata

Source index: [Cloud system tables](https://docs.dremio.com/dremio-cloud/sql/system-tables/).
These runtime system tables are read-only. Querying them requires `ADMIN` or
`SELECT` on the specific runtime system table.

## Organization and project security

| Object | Scope and purpose | Source |
| --- | --- | --- |
| `sys.organization.privileges` | Privilege metadata at organization level. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/privileges-organization/) |
| `sys.project.privileges` | Privilege metadata at project level. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/privileges-project/) |
| `sys.organization.roles` | Roles in an organization. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/roles/) |
| `sys.organization.users` | Users in an organization. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/users/) |

```sql
SELECT grantee_id, privilege, object_type
FROM sys.project.privileges;
```

## Project objects

| Object | Scope and constraint | Source |
| --- | --- | --- |
| `sys.project."tables"` | Table metadata in a project. `"tables"` must be quoted because `TABLES` is reserved; rows can be absent without access to the metadata storage container. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/tables/) |
| `sys.project.views` | View metadata in a project; rows can be absent without access to the metadata storage container. | [docs](https://docs.dremio.com/dremio-cloud/sql/system-tables/views/) |

```sql
SELECT table_name, type
FROM sys.project."tables";
```

The organization and project privilege tables are distinct published objects;
choose the table that matches the privilege scope being inspected.
