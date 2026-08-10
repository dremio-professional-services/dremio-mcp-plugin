# Information Schema

Source: [Enterprise Information Schema](https://docs.dremio.com/current/reference/sql/information-schema/).
These ANSI-based, system-generated views are read-only: users cannot modify or
drop them.

| View | Published metadata and constraint | Source |
| --- | --- | --- |
| `INFORMATION_SCHEMA.CATALOGS` | Catalog metadata; always one row and `CATALOG_NAME` is `DREMIO`. | [docs](https://docs.dremio.com/current/reference/sql/information-schema/catalogs/) |
| `INFORMATION_SCHEMA.COLUMNS` | Columns in tables and views. Table-column listings follow each source's metadata-caching policy and are not refreshed if data is expired. | [docs](https://docs.dremio.com/current/reference/sql/information-schema/columns/) |
| `INFORMATION_SCHEMA.SCHEMATA` | Sources, spaces, and embedded folders that contain datasets. | [docs](https://docs.dremio.com/current/reference/sql/information-schema/schemata/) |
| `INFORMATION_SCHEMA."TABLES"` | Tables and views. Quote `"TABLES"` so it parses as a view name rather than the reserved keyword. | [docs](https://docs.dremio.com/current/reference/sql/information-schema/tables/) |
| `INFORMATION_SCHEMA.VIEWS` | View metadata and the original defining SQL. | [docs](https://docs.dremio.com/current/reference/sql/information-schema/views/) |

```sql
SELECT table_schema, table_name, table_type
FROM INFORMATION_SCHEMA."TABLES";
```
