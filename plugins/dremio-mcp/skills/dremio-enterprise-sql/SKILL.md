---
name: dremio-enterprise-sql
description: Use when a request has SQL syntax, SQL review, system-table SQL, or metadata-query intent and both Dremio Enterprise edition and version 26.x are explicit or established context. Do not use when only self-managed Dremio is established, for broad coordinator, executor, queue, job, user, role, or operational questions without SQL or metadata-query intent, or for Dremio Community, non-Enterprise editions, non-26.x releases, Dremio Cloud, or an unspecified edition or version.
---

# Dremio Enterprise SQL

Write and explain SQL only for current Dremio Enterprise 26.x.

## Platform boundary

- Use this skill only for SQL syntax, SQL review, system-table SQL, or metadata-query work when both Dremio Enterprise edition and version 26.x are explicit in the request or established context.
- Self-managed Dremio alone is insufficient. If the edition or version is missing, clarify it before loading detailed references.
- Do not trigger on broad mentions of coordinators, executors, workload queues, jobs, users, roles, or platform operations without SQL or metadata-query intent.
- Do not use this skill for Dremio Community, non-Enterprise editions, non-26.x releases, or Dremio Cloud.
- If the platform is unspecified, ask whether the target is current Dremio Cloud or Dremio Enterprise 26.x before loading detailed references.
- Do not borrow syntax, namespaces, or availability claims from Dremio Cloud.

## Workflow

1. Identify the smallest topic that answers the request.
2. Read one primary reference from the routing table.
3. Read another reference only when the request genuinely crosses topics.
4. Never load the entire `references/` directory.
5. Return syntax first, then constraints, a minimal example, and the public documentation link when useful.

## Reference routing

| Request topic | Reference |
|---|---|
| SELECT, joins, grouping, windows, CTEs | [query-select.md](references/query-select.md) |
| Object DDL | [commands-ddl.md](references/commands-ddl.md) |
| INSERT, UPDATE, DELETE, MERGE | [commands-dml.md](references/commands-dml.md) |
| Iceberg and table maintenance | [commands-iceberg.md](references/commands-iceberg.md) |
| Catalog and namespaces | [commands-catalog.md](references/commands-catalog.md) |
| Roles, users, grants, revokes | [commands-security.md](references/commands-security.md) |
| Queue and session routing | [commands-session-routing.md](references/commands-session-routing.md) |
| Types, literals, casts | [data-types.md](references/data-types.md) |
| Identifiers and keywords | [identifiers-keywords.md](references/identifiers-keywords.md) |
| Aggregate, window, percentile functions | [functions-aggregate-window.md](references/functions-aggregate-window.md) |
| Boolean, conditional, conversion functions | [functions-conditional-conversion.md](references/functions-conditional-conversion.md) |
| Date and time functions | [functions-date-time.md](references/functions-date-time.md) |
| String and regular-expression functions | [functions-string-regex.md](references/functions-string-regex.md) |
| Math and bitwise functions | [functions-math-bitwise.md](references/functions-math-bitwise.md) |
| Binary and cryptography functions | [functions-binary-crypto.md](references/functions-binary-crypto.md) |
| Semi-structured and complex functions | [functions-complex.md](references/functions-complex.md) |
| Geospatial and directory functions | [functions-geospatial-directory.md](references/functions-geospatial-directory.md) |
| System functions | [functions-system.md](references/functions-system.md) |
| AI functions | [functions-ai.md](references/functions-ai.md) |
| Jobs, history, usage | [metadata-jobs-usage.md](references/metadata-jobs-usage.md) |
| Reflection metadata | [metadata-reflections.md](references/metadata-reflections.md) |
| Security and catalog metadata | [metadata-security-catalog.md](references/metadata-security-catalog.md) |
| Cluster and version metadata | [metadata-platform.md](references/metadata-platform.md) |
| Information Schema | [metadata-information-schema.md](references/metadata-information-schema.md) |
| Table functions | [metadata-table-functions.md](references/metadata-table-functions.md) |
| Enterprise-specific SQL availability | [platform-features.md](references/platform-features.md) |

## Answer rules

- Preserve documented quoting, namespaces, object prerequisites, and privilege requirements.
- Distinguish syntax validity from whether a source, table type, or feature supports the operation.
