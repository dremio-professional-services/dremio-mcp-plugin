# Server-side AI tools on Dremio Cloud

Dremio Cloud publishes its own AI tools through the project API
(`/v1/projects/<project-id>/ai/tools`). The backend decides the list, so the
tools below are typical examples, not a fixed contract: they can differ by
project and entitlement and change over time. Always call
`DiscoverDynamicTools` for the current names, descriptions, and input schemas.
This file covers Dremio Cloud only.

## How to reach them from this plugin

The plugin starts the server over stdio. In that transport the server does not
list these tools directly; `DREMIOAI_DREMIO__ENABLE_REMOTE_TOOLS` only affects
the streamable-HTTP transport. Add `DYNAMIC_REMOTE_TOOLS` to the server mode
before starting the agent:

```bash
export DREMIOAI_TOOLS__SERVER_MODE=FOR_SELF,FOR_DATA_PATTERNS,DYNAMIC_REMOTE_TOOLS
```

The server then offers four more local tools:

| Tool | Purpose |
|---|---|
| `DiscoverDynamicTools` | Lists the server-side tools with descriptions and input schemas. The response is large. |
| `CallDynamicTool` | Invokes one server-side tool: `tool_name`, and `tool_arguments` as a dict or JSON string. |
| `SearchMetrics` | Shortcut for `searchMetrics`; needs the semantic layer (`dremio.enable_semantic_layer`). |
| `GetTableRelationships` | Shortcut for `getTableRelationships`; needs the semantic layer. |

## Read-only tools

| Tool | Parameters | Purpose |
|---|---|---|
| `runSql` | `sqlText` | Runs a SQL query. Reports "no active engine found" when no engine is running. |
| `validateSql` | `sqlText` | Lightweight correctness check for generated SQL before execution. |
| `runExplainSql` | `sqlText` | Runs `EXPLAIN PLAN FOR` the statement; pass the SQL without that prefix. |
| `parseSql` | `sqlText`, `minStageLength`, `expressionOnly` | Splits SQL into stages such as CTEs, subqueries, and function calls. |
| `selectFromInfoSchema` | `sqlText` | Runs a `SELECT` on `INFORMATION_SCHEMA` tables only. |
| `searchViewsAndTables` | `queries`, `topN`, `excludeMetrics` | Finds tables, views, and matching semantic-layer metrics. |
| `searchMetrics` | `query`, `topN` | Finds semantic-layer metrics. |
| `getTableOrViewSchema` | `path`, `includeExtendedInformation` | Returns field names and types; extended form adds column descriptions and key flags. |
| `getTableRelationships` | `path` | Returns declared and inferred join relationships with join columns and cardinality. |
| `getSampleValues` | `tablePath`, `columnName` | Returns sample values of one column. Use sparingly. |
| `getLineage` | `path`, `depth` | Returns upstream and downstream lineage; `depth` `-1` is full lineage. |
| `getWiki` | `path` | Returns the wiki text of a dataset, source, space, or folder. |
| `listFunctions` | `pattern` | Lists supported SQL functions that match a Java regular expression. |
| `getFunctionDescription` | `functionName` | Describes one SQL function and its parameters. |
| `searchSqlRecipes` | `functionNames` | Returns curated SQL recipes for the planned non-aggregate functions. |
| `listEngines` | none | Lists engines with size, state, replicas, and limits. |
| `getEngine` | `engineNameOrId` | Returns one engine with the same fields. |
| `analyzeQueryProfile` | `jobId`, `attempt` | Analyzes a job profile: operator statistics, bottlenecks, skew. |
| `searchVisualizations` | `query` | Finds saved visualizations by title or keywords. |
| `getVisualizationContext` | `entityId`, `path` | Returns identifier, version tag, SQL, title, and chart spec of a saved visualization. |
| `getFilePreviewRows` | `file_id`, `file_format`, `max_rows`, `columns` | Reads sample rows of a staged uploaded file. |

## Write tools

These change catalog objects. Use them only when the user explicitly asks, and
confirm first. Whether `DREMIOAI_DREMIO__ALLOW_DML=false` blocks them through
`CallDynamicTool` was not verified; treat them as write-capable regardless.

| Tool | Parameters | Effect |
|---|---|---|
| `createWiki` | `path`, `description` | Creates a wiki (Markdown) on a dataset, source, space, or folder. |
| `updateWiki` | `path`, `description` | Replaces an existing wiki. |
| `deleteWiki` | `path` | Deletes a wiki. |
| `addLabels` | `path`, `labels` | Appends labels to a dataset. |
| `updateLabels` | `path`, `labels` | Replaces the full label set of a dataset. |
| `deleteLabels` | `path`, `labels` | Removes the listed labels from a dataset. |
| `createIcebergTableFromFile` | `fileId`, `tableNamespace`, `fileFormat` | Creates an Iceberg table from a staged uploaded file. |

## Overlap with local tools

Several server-side tools cover the same ground as local tools:

| Server-side | Local |
|---|---|
| `runSql` | `RunSqlQuery` |
| `getTableOrViewSchema` | `GetSchemaOfTable` |
| `getLineage` | `GetTableOrViewLineage` |
| `searchViewsAndTables` | `SearchTableAndViews` |
| `getWiki` | `GetDescriptionOfTableOrSchema` |

Prefer the local tool when both are available: it needs no discovery call and
`RunSqlQuery` reports truncation. Use the server-side tools for what the local
set lacks: SQL validation and explain, function and recipe lookup, sample
values, engines, job-profile analysis, relationships, metrics, wikis, and
labels.
