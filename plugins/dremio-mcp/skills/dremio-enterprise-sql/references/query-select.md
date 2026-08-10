# SELECT, query composition, and time travel

Primary syntax and clause order: https://docs.dremio.com/current/reference/sql/commands/SELECT-statements/

## Core form

```sql
[ WITH <common_table_expression> ]
SELECT [ ALL | DISTINCT ] <select_list>
FROM <table_or_view_or_table_function>
  [ AT { REFERENCE | BRANCH } <reference_name> ]
  [ { PIVOT | UNPIVOT } (<expression>) ]
  [ <join_expression> ]
  [ WHERE <condition> ]
  [ GROUP BY <expression> ]
  [ QUALIFY <expression> ]
  [ ORDER BY <column_or_expression> [ DESC ] ]
  [ LIMIT <count> ]
  [ AT { SNAPSHOT '<snapshot_id>' | <timestamp_expression> } ]
```

`FROM` accepts a table, view, Iceberg metadata table through the `TABLE` form,
or the `UNNEST` form; use the linked page for each complete production. A `QUALIFY`
expression requires a window function in the SELECT list or the QUALIFY
expression. The current page documents CTEs, joins, grouping, `QUALIFY`, and
`PIVOT`/`UNPIVOT`. It does not establish a `HAVING` or set-operator production;
do not attribute either to this reference. Its window-function statement is
limited to `QUALIFY`: a window function must occur in SELECT or QUALIFY.

## Version and snapshot boundary

`AT REFERENCE` / `AT BRANCH` is the version-context form for a Nessie source.
`AT SNAPSHOT '<snapshot_id>'` and `AT <timestamp_expression>` are documented
Iceberg time-travel forms. The latter accepts any SQL expression resolving to
one TIMESTAMP value, such as `CAST(DATE_SUB(CURRENT_DATE, 1) AS TIMESTAMP)`.
Use them only with an Iceberg table and supporting source; they are not general
query-history features.

```sql
SELECT order_id
FROM lake.orders AT CAST(DATE_SUB(CURRENT_DATE, 1) AS TIMESTAMP);
```
