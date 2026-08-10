# Enterprise object DDL and reflections

Current command index: https://docs.dremio.com/current/reference/sql/commands/

In this file, `*` means repeat the preceding bracketed list zero or more times;
it avoids abbreviating documented list syntax with an ellipsis.

## Tables and views

Primary pages: [CREATE TABLE](https://docs.dremio.com/current/reference/sql/commands/create-table/),
[CTAS](https://docs.dremio.com/current/reference/sql/commands/create-table-as/),
[tables](https://docs.dremio.com/current/reference/sql/commands/tables),
[CREATE VIEW](https://docs.dremio.com/current/reference/sql/commands/create-view/),
[ALTER VIEW](https://docs.dremio.com/current/reference/sql/commands/alter-view/), and
[DROP VIEW](https://docs.dremio.com/current/reference/sql/commands/drop-view/).

```sql
CREATE TABLE [ IF NOT EXISTS ] <table_name>
  ( <column_name> <data_type> [ { NULL | NOT NULL } ]
    [, <column_name> <data_type> [ { NULL | NOT NULL } ] ]* )
  [ MASKING POLICY <function_name> ( <column_name> [, <column_name> ]* ) ]
  [ ROW ACCESS POLICY <function_name> ( <column_name> [, <column_name> ]* ) ]
  [ PARTITION BY ( { <column_name> | <partition_transform> }
    [, { <column_name> | <partition_transform> } ]* ) ]
  [ CLUSTER BY ( <column_name> [, <column_name> ]* ) ]
  [ LOCALSORT BY ( <column_name> [, <column_name> ]* ) ]
  [ TBLPROPERTIES ( '<property_name>' = '<property_value>'
    [, '<property_name>' = '<property_value>' ]* ) ];

CREATE TABLE [ IF NOT EXISTS ] <table_name>
  [ ( <column_name> <data_type> [ { NULL | NOT NULL } ]
    [, <column_name> <data_type> [ { NULL | NOT NULL } ] ]* ) ]
  [ PARTITION BY ( { <column_name> | <partition_transform> }
    [, { <column_name> | <partition_transform> } ]* ) ]
  [ CLUSTER BY ( <column_name> [, <column_name> ]* ) ]
  [ LOCALSORT BY ( <column_name> [, <column_name> ]* ) ]
  [ TBLPROPERTIES ( '<property_name>' = '<property_value>'
    [, '<property_name>' = '<property_value>' ]* ) ]
  AS <select_statement>;

CREATE [ OR REPLACE ] VIEW <view_name> AS <select_statement> FROM <table_name>;
DESCRIBE TABLE <table_name>;
DROP TABLE <source>.<tableName>;
DROP VIEW [ IF EXISTS ] <view_name>;
```

`MASKING POLICY` requires a UDF with matching input/output type; `ROW ACCESS
POLICY` requires a UDF returning BOOLEAN. In this Enterprise-platform reference,
both features require the corresponding Enterprise-edition entitlement; that
licensing statement does not establish whether Dremio Cloud publishes comparable
forms. Partition transforms apply only to Iceberg tables. `CLUSTER BY` likewise
requires the Enterprise-edition entitlement and cannot be combined with
`PARTITION BY` or `LOCALSORT BY`. CTAS is enabled per source and requires the
relevant source privileges. `DROP TABLE` is documented only for tables created
on a filesystem source and requires permission.
Replacement and drop forms change or remove objects.

For a current Iceberg REST Catalog view, the documented metadata form is:

```sql
ALTER VIEW <view_name> [ AT { REF[ERENCE] | BRANCH } <reference_name> ]
  REFRESH METADATA
    [ FOR PARTITIONS ( <partition_name> = '<value>' ) ]
    [ { AVOID | AUTO } PROMOTION ]
    [ { FORCE | LAZY } UPDATE ]
    [ { MAINTAIN | DELETE } WHEN MISSING ];
```

`REFRESH METADATA` does not support views in Spaces. If several refresh
options are supplied, the current page requires promotion, then update, then
missing-data order.

## ALTER TABLE and definition inspection

Sources: [ALTER TABLE](https://docs.dremio.com/current/reference/sql/commands/alter-table/),
[SHOW CREATE TABLE](https://docs.dremio.com/current/reference/sql/commands/show-create-table/),
[SHOW CREATE VIEW](https://docs.dremio.com/current/reference/sql/commands/show-create-view/), and
[SHOW TBLPROPERTIES](https://docs.dremio.com/current/reference/sql/commands/show-table-properties/).

```sql
ALTER TABLE <table_name>
  { ADD PRIMARY KEY ( <column_name> [, <column_name> ]* )
  | DROP PRIMARY KEY
  | ADD COLUMNS ( <column_name> <data_type> [ NULL ]
    [, <column_name> <data_type> [ NULL ] ]* )
  | DROP COLUMN <column_name>
  | { ALTER | MODIFY | CHANGE } COLUMN <old_name> <new_name> <data_type>
    [ { NULL | NOT NULL | DROP NOT NULL } ]
  | MODIFY COLUMN <column_name>
    { SET MASKING POLICY <function_name> ( <column_name> [, <column_name> ]* )
    | UNSET MASKING POLICY <function_name> }
  | { ADD | DROP } ROW ACCESS POLICY <function_name>
    ( <column_name> [, <column_name> ]* )
  | CLUSTER BY ( <column_name> [, <column_name> ]* )
  | DROP CLUSTERING KEY
  | LOCALSORT BY ( <column_name> [, <column_name> ]* )
  | REFRESH METADATA
    [ FOR PARTITIONS ( <partition_name> = '<value>' ) ]
    [ { AVOID | AUTO } PROMOTION ]
    [ { FORCE | LAZY } UPDATE ]
    [ { MAINTAIN | DELETE } WHEN MISSING ]
  | FORGET METADATA
  | SET TBLPROPERTIES ( '<property_name>' = '<property_value>'
    [, '<property_name>' = '<property_value>' ]* )
  | UNSET TBLPROPERTIES ( '<property_name>' [, '<property_name>' ]* )
  | { ENABLE | DISABLE } { RAW | AGGREGATE } ACCELERATION
  | { ADD | DROP } PARTITION FIELD { <column_name> | <partition_transform> } };

SHOW CREATE TABLE <table_name>
  [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT } <reference_name> ];
SHOW CREATE VIEW <view_name>
  [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT } <reference_name> ];
SHOW TBLPROPERTIES <table_name>;
```

The exact reflection alternatives of `ALTER TABLE` are in the Reflection
lifecycle section below. Primary keys apply only to Apache Iceberg tables and
do not enforce uniqueness. Dropping a column cannot be undone. A rename is not
supported for Parquet, JSON, or BSON, and primitive type changes are limited to
`INT` to `BIGINT`, `FLOAT` to `DOUBLE`, or widening DECIMAL precision with the
same scale. Metadata-refresh option order is promotion, update, then missing.

## User-defined functions

Source: https://docs.dremio.com/current/reference/sql/commands/functions

```sql
CREATE [ OR REPLACE ] FUNCTION [ IF NOT EXISTS ] <function_name>
  ( [ <parameter_name> <data_type> [, <parameter_name> <data_type> ]* ] )
  RETURNS <data_type>
  RETURN { <expression> | <query> };

CREATE [ OR REPLACE ] FUNCTION [ IF NOT EXISTS ] <function_name>
  ( [ <parameter_name> <data_type> [, <parameter_name> <data_type> ]* ] )
  RETURNS TABLE ( <column_name> <data_type> [, <column_name> <data_type> ]* )
  RETURN <query>;

SHOW FUNCTIONS [ LIKE { <pattern> } ];
{ DESC | DESCRIBE } FUNCTION <function_name>;
DROP FUNCTION [ IF EXISTS ] <function_name>;
```

`OR REPLACE` and `IF NOT EXISTS` are mutually exclusive. A scalar UDF may
return an expression or query; a tabular UDF may return only a query and is
used only in `FROM`. Only the UDF owner may drop it.

## Reflection lifecycle

Source: https://docs.dremio.com/current/reference/sql/commands/acceleration

```sql
ALTER { DATASET | TABLE | VIEW } <dataset_name>
  CREATE AGGREGATE REFLECTION <reflection_name> USING
    { DIMENSIONS ( <column_name> [, <column_name> ]* )
    | MEASURES ( <column_name> ( <aggregation_type> [, <aggregation_type> ]* )
      [, <column_name> ( <aggregation_type> [, <aggregation_type> ]* ) ]* )
    | DIMENSIONS ( <column_name> [, <column_name> ]* )
      MEASURES ( <column_name> ( <aggregation_type> [, <aggregation_type> ]* )
      [, <column_name> ( <aggregation_type> [, <aggregation_type> ]* ) ]* ) }
    [ PARTITION BY ( <column_name_or_partition_transform> [, <column_name_or_partition_transform> ]* ) ]
    [ LOCALSORT BY ( <column_name> [, <column_name> ]* ) ]
    [ ARROW CACHE ];

ALTER { DATASET | TABLE | VIEW } <dataset_name>
  CREATE EXTERNAL REFLECTION <reflection_name> USING <table_name>;

ALTER { DATASET | TABLE | VIEW } <dataset_name>
  CREATE RAW REFLECTION <reflection_name>
  USING DISPLAY ( <column_name> [, <column_name> ]* )
  [ PARTITION BY ( <column_name_or_partition_transform> [, <column_name_or_partition_transform> ]* ) ]
  [ LOCALSORT BY ( <column_name> [, <column_name> ]* ) ]
  [ ARROW CACHE ];

ALTER { DATASET | TABLE | VIEW } <dataset_name>
  { DROP REFLECTION <reflection_name>
  | REFRESH REFLECTIONS
  | ROUTE REFLECTIONS TO { DEFAULT QUEUE | QUEUE { <queue_name> | <queue_uuid> } } };
```

The current page also documents `{ ADD | DROP } PARTITION FIELD
{ <column_name> | <partition_transform> }` for the same `ALTER` subject.
For `ALTER VIEW`, its reflection alternatives omit `ARROW CACHE` and it also
supports the view metadata-refresh form above. Reflection creation, drop,
refresh, and queue routing alter acceleration behavior; validate the target and
queue before execution.
