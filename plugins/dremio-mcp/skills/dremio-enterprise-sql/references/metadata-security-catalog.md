# Security and catalog metadata

Source index: [Enterprise system tables](https://docs.dremio.com/current/reference/sql/system-tables/).
All objects below are read-only. The current index says administrators use
`GRANT` and `REVOKE` for system tables that support delegated access.

For a delegable system table, use the current [GRANT/REVOKE syntax](https://docs.dremio.com/current/reference/sql/commands/rbac/):

```sql
GRANT SELECT ON TABLE <sys.table> TO { USER | ROLE } <principal>;
REVOKE SELECT ON TABLE <sys.table> FROM { USER | ROLE } <principal>;
```

Neutral delegated-access example:

```sql
REVOKE SELECT ON TABLE sys.views FROM ROLE <principal>;
```

## Public access-statement boundary

The dedicated pages for [`sys.users`](https://docs.dremio.com/current/reference/sql/system-tables/users/),
[`sys.roles`](https://docs.dremio.com/current/reference/sql/system-tables/roles/), and
[`sys.privileges`](https://docs.dremio.com/current/reference/sql/system-tables/privileges/)
describe each object and its columns but do not publish an access matrix. The
central [system-table index](https://docs.dremio.com/current/reference/sql/system-tables/)
says administrators can delegate access to all system tables except
`sys.copy_errors_history`, `sys.copy_file_history`, and `sys.pipe_summary`; by
that general statement, these three are delegable. The central
[GRANT/REVOKE page](https://docs.dremio.com/current/reference/sql/commands/rbac/)
also says `sys.privileges` is viewable only by administrators. That conflicts
with the index for `sys.privileges`; the dedicated pages make no statement that
resolves it. For `sys.users` and `sys.roles`, the public pages provide only the
index's general delegation statement, not an exhaustive per-table access rule.
Do not infer a complete access matrix from these pages.

| Object | Published purpose | Source |
| --- | --- | --- |
| `sys.users` | Users in the Dremio instance. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/users/) |
| `sys.roles` | Roles in the Dremio instance. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/roles/) |
| `sys.membership` | Role membership metadata. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/membership/) |
| `sys.privileges` | Object-privilege metadata. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/privileges/) |
| `sys."tables"` | Table metadata. Quote `"tables"`: `TABLES` is a reserved keyword. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/tables/) |
| `sys.views` | View metadata. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/views/) |
| `sys.user_defined_functions` | Installed user-defined-function metadata. A `1970-01-01 00:00:00.000` timestamp means never used or set. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/user-defined-functions/) |

```sql
SELECT table_name, type
FROM sys."tables";
```
