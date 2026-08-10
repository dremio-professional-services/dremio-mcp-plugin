# Apache Iceberg row changes

Current mutation index: https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/

## INSERT

Source: https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/apache-iceberg-insert/

```sql
INSERT INTO <table_name>
  [ AT { REF[ERENCE] | BRANCH } <reference_name> ]
  [ ( <column_name> [, <column_name> ]* ) ]
  { <select_statement>
  | VALUES ( <value> [, <value> ]* ) [, ( <value> [, <value> ]* ) ]* };
```

The version clause is only for Nessie sources; if omitted, the current branch
is used. With an explicit column list, values are mapped in that listed order;
otherwise Dremio uses the table column order.

## UPDATE and DELETE

Sources: [UPDATE](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/apache-iceberg-update/)
and [DELETE](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/apache-iceberg-delete/).

```sql
UPDATE <table_name>
  [ AT { REF[ERENCE] | BRANCH } <reference_name> ]
  [ AS <alias> ]
  SET <column_name> = <value> [, <column_name> = <value> ]*
  [ FROM <additional_table_or_query> [, <additional_table_or_query> ] ]
  [ WHERE <where_conditions> ];

DELETE FROM <table_name>
  [ AT { REF[ERENCE] | BRANCH } <reference_name> ]
  [ AS <alias> ]
  [ USING <additional_table_or_query> [, <additional_table_or_query> ] ]
  [ WHERE <where_conditions> ];
```

Both version clauses are Nessie-only and default to the current branch. An
unqualified `UPDATE` or `DELETE` condition can affect every target row. When a
target table reference is supplied and an additional source is used, use the
corresponding reference for that source as required by the current command
page.

## MERGE and TRUNCATE

Sources: [MERGE](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/apache-iceberg-merge/)
and [TRUNCATE](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/apache-iceberg-truncate/).

```sql
MERGE INTO <target_table_name>
  [ AT { REF[ERENCE] | BRANCH } <reference_name> ]
  [ AS <target_alias> ]
USING { ( <select_statement> ) | <source_table_name> [ AS <source_alias> ] }
ON ( <condition> )
  [ WHEN MATCHED THEN
      { UPDATE SET *
      | UPDATE SET <column_name> = <value> [, <column_name> = <value> ]* } ]
  [ WHEN NOT MATCHED THEN
      { INSERT *
      | INSERT ( <column_name> [, <column_name> ]* )
        VALUES ( <expression> [, <expression> ]* ) } ];

TRUNCATE [ TABLE ] [ IF EXISTS ] <table_path>.<table_name>
  [ AT BRANCH <branch_name> ];
```

`MERGE` accepts either a parenthesized SELECT source or a table source. `UPDATE
SET *` and `INSERT *` are current documented alternatives. `TRUNCATE` removes
all rows; `TABLE`, `IF EXISTS`, and `AT BRANCH` retain the meanings on its
current page. These commands apply to Apache Iceberg tables, not arbitrary
datasets or sources.
