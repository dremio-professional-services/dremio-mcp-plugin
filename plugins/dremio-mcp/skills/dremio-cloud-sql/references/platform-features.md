# Cloud SQL platform boundaries

Use these Cloud-only SQL-visible distinctions to avoid importing Enterprise
syntax or availability claims. Each row is limited to published Cloud SQL
documentation.

| Cloud distinction | SQL guidance | Source |
| --- | --- | --- |
| System-table namespaces | The index has organization-level `sys.organization` and `sys.organization.history` objects, and project-level `sys.project` and `sys.project.history` objects. `sys.project.copy_errors_history` and `sys.project.materializations` are historical index entries with exceptional names, so not every historical table is under `.history`. | [Cloud system tables](https://docs.dremio.com/dremio-cloud/sql/system-tables/) |
| Engine routing | `SET ENGINE` selects the engine for the current session and requires `USAGE`; `RESET ENGINE` removes the session override. | [SET ENGINE](https://docs.dremio.com/dremio-cloud/sql/commands/set-engine/) |
| Object namespaces | `CREATE TABLE` allows a table inside an existing namespace such as a folder; create that namespace first. | [CREATE TABLE](https://docs.dremio.com/dremio-cloud/sql/commands/create-table/) |
| Reserved-word object names | Enclose a reserved keyword used as an object name in double quotes. | [Cloud reserved keywords](https://docs.dremio.com/dremio-cloud/sql/keywords/) |
| UUID | `UUID` is available only for Apache Iceberg tables and does not enforce uniqueness. | [Cloud data types](https://docs.dremio.com/dremio-cloud/sql/data-types/) |
| VARIANT | `VARIANT` is available only for Apache Iceberg v3 tables. | [Cloud data types](https://docs.dremio.com/dremio-cloud/sql/data-types/) |
| AI functions | The public Cloud AI category lists `AI_CLASSIFY`, `AI_COMPLETE`, `AI_GENERATE`, and `LIST_FILES`. | [Cloud AI functions](https://docs.dremio.com/dremio-cloud/sql/sql-functions/AI/) |

Do not infer unlisted Cloud syntax or feature availability from another Dremio
edition.
