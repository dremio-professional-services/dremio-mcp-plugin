# Platform metadata

Source index: [Enterprise system tables](https://docs.dremio.com/current/reference/sql/system-tables/).
The system tables below are read-only. For a system table that supports
delegated access, the current index uses `GRANT` and `REVOKE`.

For a delegable system table, use the current [GRANT/REVOKE syntax](https://docs.dremio.com/current/reference/sql/commands/rbac/):

```sql
GRANT SELECT ON TABLE <sys.table> TO { USER | ROLE } <principal>;
REVOKE SELECT ON TABLE <sys.table> FROM { USER | ROLE } <principal>;
```

| Object | Published purpose | Source |
| --- | --- | --- |
| `sys.version` | Version metadata for the deployed Dremio Enterprise instance. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/version/) |
| `sys.timezone_names` | Complete timezone list and associated offset/daylight-saving information. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/timezone-names/) |
| `sys.pipes` | Autoingest-pipe metadata. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/pipes/) |
| `sys.engines` | Metadata for engines in the Dremio instance. | [docs](https://docs.dremio.com/current/reference/sql/system-tables/engines/) |

```sql
SELECT version, build_time
FROM sys.version;
```

This metadata is distinct from session queue and tag routing; use the routing
commands for changes.
