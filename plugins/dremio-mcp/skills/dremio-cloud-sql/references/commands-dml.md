# Row-changing commands

Sources: [INSERT](https://docs.dremio.com/dremio-cloud/sql/commands/insert/),
[UPDATE](https://docs.dremio.com/dremio-cloud/sql/commands/update/),
[DELETE](https://docs.dremio.com/dremio-cloud/sql/commands/delete/),
[MERGE](https://docs.dremio.com/dremio-cloud/sql/commands/merge/), and
[TRUNCATE](https://docs.dremio.com/dremio-cloud/sql/commands/truncate/).

## INSERT

```sql
INSERT INTO <table_name> [ (<column_name> [, ...]) ]
{ VALUES (<expression> [, ...]) [, ...] | <select_statement> };
```

With an explicit column list, supplied values map in that order. Without one,
the values must match the target table definition. A query form inserts the
result set into the target.

```sql
INSERT INTO lakehouse.orders (order_id, amount)
VALUES (1001, 42.50);
```

## UPDATE and DELETE

```sql
UPDATE <table_name> [ AS <alias> ]
SET <column1_name> = <value1> [, <column_name2> = <value2> ...]
[ WHERE <where_conditions> ];

DELETE FROM <table_name> [ AS <alias> ]
[ USING <additional_table_or_query> ]
[ WHERE <where_conditions> ];
```

`AS <alias>` aliases the target. `UPDATE` values may be expressions or
single-value subqueries, and must satisfy any target-column `NOT NULL`
constraints. The public page's additional `FROM` form is demonstrated exactly
below. `DELETE ... USING` supplies additional tables or parenthesized
subqueries for the `WHERE` condition. Omitting `WHERE` affects every target
row. The public pages describe copy-on-write as the default mode and link the
`write.update.mode` and `write.delete.mode` Iceberg properties for
merge-on-read configuration.

```sql
UPDATE MYSOURCE.MYTABLE
SET EXPR$0 = s.EXPR$1
FROM MYSOURCE.MYTABLE2 AS s;

DELETE FROM orders USING returns
WHERE orders.order_id = returns.order_id;
```

## MERGE

```sql
MERGE INTO <target_table> [ AS <target_alias> ]
USING <source_table_or_query> [ AS <source_alias> ]
ON <match_condition>
[ WHEN MATCHED THEN
    UPDATE SET *
  | UPDATE SET <column_name> = <expression> [, ...] ]
[ WHEN NOT MATCHED THEN
    INSERT *
  | INSERT (<column_name> [, ...]) VALUES (<expression> [, ...]) ];
```

At least one `WHEN` branch is required. Each branch is independently optional,
so a statement may update only, insert only, or do both. `UPDATE SET *` and
`INSERT *` require compatible source and target column layouts. Prefer an
explicit mapping when schemas differ. The current public page labels the
insert-all parameter `INSERT SET *`, but its grammar and second example use
`INSERT *`; this reference follows the grammar and example.

```sql
MERGE INTO lakehouse.orders AS target
USING staging.orders AS source
ON target.order_id = source.order_id
WHEN MATCHED THEN UPDATE SET amount = source.amount
WHEN NOT MATCHED THEN INSERT (order_id, amount)
VALUES (source.order_id, source.amount);
```

## TRUNCATE

```sql
TRUNCATE [ TABLE ] [ IF EXISTS ] <table_name>;
```

`TRUNCATE` removes all rows with less computation than a row-by-row delete.
It is not supported on AWS Glue datasources. `TABLE` is optional; `IF EXISTS`
prevents an error when the table does not exist. Confirm the target datasource
and table before use.
