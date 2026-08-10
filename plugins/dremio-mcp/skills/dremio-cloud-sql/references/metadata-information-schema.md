# Information Schema

Source: [Cloud Information Schema](https://docs.dremio.com/dremio-cloud/sql/information-schema/).
Information Schema views are system-generated and read-only: users cannot
modify or drop them. They contain project metadata and are based on ANSI
Information Schema.

| View | Returned metadata and constraint | Source |
| --- | --- | --- |
| `INFORMATION_SCHEMA.CATALOGS` | The project metadata catalog; it always has one row and `CATALOG_NAME` is always `DREMIO`. | [docs](https://docs.dremio.com/dremio-cloud/sql/information-schema/catalogs/) |
| `INFORMATION_SCHEMA.COLUMNS` | Columns of project tables and views. Table-column results follow each source's metadata-caching policy and can be incomplete without access to the metadata storage container. | [docs](https://docs.dremio.com/dremio-cloud/sql/information-schema/columns/) |
| `INFORMATION_SCHEMA.SCHEMATA` | Project sources, spaces, and embedded folders that contain datasets. | [docs](https://docs.dremio.com/dremio-cloud/sql/information-schema/schemata/) |
| `INFORMATION_SCHEMA."TABLES"` | Project tables and views. `"TABLES"` must be quoted because `TABLES` is reserved; rows can be absent without access to the metadata storage container. | [docs](https://docs.dremio.com/dremio-cloud/sql/information-schema/tables/) |
| `INFORMATION_SCHEMA.VIEWS` | Project view metadata; rows can be absent without access to the metadata storage container. | [docs](https://docs.dremio.com/dremio-cloud/sql/information-schema/views/) |

```sql
SELECT table_schema, table_name, table_type
FROM INFORMATION_SCHEMA."TABLES";
```
