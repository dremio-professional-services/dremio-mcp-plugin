# Local MCP tools

Tools that the upstream [`dremio/dremio-mcp`](https://github.com/dremio/dremio-mcp)
server itself provides over stdio. The plugin does not pin the upstream
version, so the tool set can change; the tools the session offers are
authoritative. Claude Code prefixes the names
with `mcp__plugin_dremio-mcp_dremio-mcp__`.

## Tools and requirements

| Tool | Purpose | Available when |
|---|---|---|
| `RunSqlQuery` | Runs one SQL statement and returns rows as JSON. | `SERVER_MODE` includes `FOR_SELF` or `FOR_DATA_PATTERNS` |
| `GetSchemaOfTable` | Returns columns and types of a table or view, plus wiki text and tags if present. | Same |
| `GetDescriptionOfTableOrSchema` | Returns wiki description and tags of tables, schemas, and their parent schemas. | Same |
| `GetTableOrViewLineage` | Returns upstream and downstream objects of a table or view (ids, paths, types; no columns). | Same |
| `GetUsefulSystemTableNames` | Lists system tables worth querying, such as `INFORMATION_SCHEMA."TABLES"` and job history. | Same |
| `SearchTableAndViews` | Semantic search for tables and views; results include schema, tags, description, and optional relationships and metrics. | Same, plus `DREMIOAI_DREMIO__ENABLE_SEARCH=true` |
| `BuildUsageReport` | Builds a 7-day usage report grouped by `PROJECT` or `ENGINE`. | `SERVER_MODE` includes `FOR_SELF` and `DREMIOAI_DREMIO__PROJECT_ID` is set (Dremio Cloud) |
| `GetRelevantMetrics`, `GetMetricSchema`, `RunPromQL` | Query Prometheus metrics of a self-managed cluster. | `SERVER_MODE` includes `FOR_PROMETHEUS` and Prometheus is configured upstream |
| `DiscoverDynamicTools`, `CallDynamicTool`, `SearchMetrics`, `GetTableRelationships` | Reach the server-side AI tools of the Dremio backend; see [dremio-cloud-ai-tools.md](dremio-cloud-ai-tools.md). | `SERVER_MODE` includes `DYNAMIC_REMOTE_TOOLS` |

With the upstream defaults (`SERVER_MODE=FOR_SELF`, search off, no project ID)
the server offers the first five tools.

## Parameters

| Tool | Parameters |
|---|---|
| `RunSqlQuery` | `query`: the SQL text |
| `GetSchemaOfTable` | `table_name`: `"source"."schema"."table"` or a list of path parts |
| `GetDescriptionOfTableOrSchema` | `name`: one name or a list of names |
| `GetTableOrViewLineage` | `table_name`: string or list of path parts |
| `GetUsefulSystemTableNames` | none |
| `SearchTableAndViews` | `query`: search text; `topN`: optional result limit |
| `BuildUsageReport` | `by`: `PROJECT` or `ENGINE` (default) |

## Usage notes

- Find data with `SearchTableAndViews` when available; otherwise query
  `INFORMATION_SCHEMA."TABLES"` through `RunSqlQuery`. Search is not
  exhaustive: it returns at most the server-side `topN` (default 10).
- Check columns with `GetSchemaOfTable` before writing SQL.
- In `RunSqlQuery`, double-quote identifiers that are SQL keywords, such as
  `"day"`, `"count"`, or `"TABLES"`.
- `RunSqlQuery` caps the response size. A result with `"truncated": true` is
  partial (`total_rows` versus `returned_rows`); aggregate, filter, or select
  fewer columns instead of treating it as complete.
- DML and DDL through `RunSqlQuery` fail unless
  `DREMIOAI_DREMIO__ALLOW_DML=true`.
- `GetTableOrViewLineage` returns no columns; call `GetSchemaOfTable` on an
  entity path for details.
- Every tool runs with the Dremio privileges of the PAT owner. A missing table
  can mean missing privileges.
