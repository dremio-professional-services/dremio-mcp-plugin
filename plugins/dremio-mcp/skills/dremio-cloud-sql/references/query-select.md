# SELECT and query composition

Source: [SELECT](https://docs.dremio.com/dremio-cloud/sql/commands/SELECT/).

## Core grammar

```sql
[ WITH ... ]
SELECT [ ALL | DISTINCT ] <select_list>
FROM <table_or_view>
[ WHERE <condition> ]
[ GROUP BY <expression> ]
[ HAVING <condition> ]
[ QUALIFY <condition> ]
[ ORDER BY <expression> [ ASC | DESC ] [, ...] ]
[ LIMIT <non_negative_integer> ]
```

`ALL` is the default; `DISTINCT` removes duplicate result rows. `WHERE`
filters input rows, `GROUP BY` defines aggregate groups, and `HAVING` filters
groups. `ORDER BY` defaults to ascending order. `LIMIT` must be a non-negative
integer.

## Joins, set operations, and nesting

Use `JOIN ... ON <condition>` (including `INNER`, `LEFT`, `RIGHT`, `FULL`, and
`CROSS` where appropriate) to combine relations. Use parenthesized subqueries
in `FROM`, predicates such as `IN` or `EXISTS`, and scalar subqueries only when
their result cardinality matches the expression context. Combine compatible
query results with `UNION [ALL]`, `INTERSECT`, or `EXCEPT`.

A CTE is a named subquery introduced by `WITH`; it scopes to the statement.

```sql
WITH regional_sales AS (
  SELECT region, SUM(amount) AS total_amount
  FROM analytics.sales
  GROUP BY region
)
SELECT region, total_amount
FROM regional_sales
ORDER BY total_amount DESC
LIMIT 10;
```

## Windows and QUALIFY

Window functions use `OVER (...)`, optionally with `PARTITION BY`, `ORDER BY`,
and a frame. `QUALIFY` filters after aggregate and window calculation; the
query must contain a window function in the select list or the `QUALIFY`
condition.

```sql
SELECT customer_id, order_id,
       ROW_NUMBER() OVER (
         PARTITION BY customer_id ORDER BY ordered_at DESC
       ) AS row_number
FROM analytics.orders
QUALIFY row_number = 1;
```

## Other documented query forms

- `FROM UNNEST(<list_expression>) [ WITH ORDINALITY ]` expands a list. The
  ordinality column can preserve element order.
- `PIVOT` and `UNPIVOT` reshape a SELECT result. Do not put an alias between
  the table or subquery and its `PIVOT` or `UNPIVOT` clause.
- `TABLE(<source>.EXTERNAL_QUERY('<select_statement>'))` delegates the quoted
  statement to a supported external source.
- `TABLE(<iceberg_metadata>(<table_name>))` exposes documented Iceberg metadata
  table functions such as table history, files, manifests, partitions, and
  snapshots.

## Iceberg and Delta Lake time travel

For Iceberg and Delta Lake tables, the public SELECT syntax documents snapshot
and timestamp forms. Use a snapshot identifier or timestamp only when the table
and catalog support the requested history:

```sql
SELECT *
FROM lakehouse.orders AT SNAPSHOT '123456789';

SELECT *
FROM lakehouse.orders AT TIMESTAMP '2025-01-01 00:00:00';
```

The snapshot and timestamp forms above are distinct from the catalog reference
selectors documented below. See the source page for the complete current
`SELECT` grammar.

## Version-context queries

The public Cloud `SELECT` syntax also supports a catalog version context on a
table or view:

```sql
<table_or_view> AT { REF[ERENCE] | BRANCH | TAG | COMMIT } <reference_name>
  [ AS OF <timestamp> ]
```

`REF` can name a branch, tag, or commit; `BRANCH`, `TAG`, and `COMMIT` select
the corresponding reference kind. When `AT` is omitted, Cloud uses the current
reference. Commit hashes must be enclosed in double quotes. `AS OF` is allowed
only with `REF`, `BRANCH`, or `TAG` (not `COMMIT`) and must resolve to one
timestamp value.

```sql
SELECT *
FROM lakehouse.orders AT BRANCH release AS OF TIMESTAMP '2025-01-01 00:00:00';

SELECT *
FROM lakehouse.orders AT COMMIT "ff2fe50fef5a030c4fc8e61b252bdc33c72e2b6f929d81383d998b8368302e2";
```

The same reference selector is published for a function name; its optional
`AS OF <timestamp>` follows the function's `AT` clause. These are query-time
selectors, not reference-management commands.
