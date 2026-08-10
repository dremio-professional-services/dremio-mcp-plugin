# Object DDL

Source: the public [SQL command index](https://docs.dremio.com/dremio-cloud/sql/commands/),
[CREATE TABLE](https://docs.dremio.com/dremio-cloud/sql/commands/create-table/),
[CREATE TABLE AS](https://docs.dremio.com/dremio-cloud/sql/commands/create-table-as/),
[ALTER TABLE](https://docs.dremio.com/dremio-cloud/sql/commands/alter-table/),
[CREATE VIEW](https://docs.dremio.com/dremio-cloud/sql/commands/create-view/),
and [CREATE FUNCTION](https://docs.dremio.com/dremio-cloud/sql/commands/create-function/).

## Tables

```sql
CREATE TABLE [ IF NOT EXISTS ] <table_name> ( <column_name> <data_type> [, ...] );
CREATE TABLE [ IF NOT EXISTS ] <table_name> AS <select_statement>;
ALTER TABLE <table_name> <alteration>;
DROP TABLE [ IF EXISTS ] <table_name>;
```

`CREATE TABLE` defines columns and supports documented table properties,
partitioning, sorting, clustering, and nullability forms. `CREATE TABLE AS`
materializes a SELECT result; use an explicit column definition when a type,
default, or `NOT NULL` constraint must be controlled. The containing namespace
must already exist. `ALTER TABLE` includes documented column, property,
partition, clustering, policy, and reflection changes. Dropping an Iceberg
table has catalog- and source-dependent effects, so confirm the source page
before using it operationally.

The Cloud pages publish `CLUSTER BY`, masking-policy, and row-access-policy
forms, but mark all of them as available only with an Enterprise-edition
entitlement. This includes `CREATE TABLE ... CLUSTER BY`, `MASKING POLICY`,
and `ROW ACCESS POLICY`, plus the corresponding `ALTER TABLE` clustering and
policy forms; do not present them as universally available in Cloud.

```sql
CREATE TABLE lakehouse.orders (
  order_id BIGINT NOT NULL,
  ordered_at TIMESTAMP,
  amount DECIMAL(12, 2)
);
```

## Views

```sql
CREATE [ OR REPLACE ] VIEW <view_name> AS <select_statement>;
ALTER VIEW <view_name> <alteration>;
DROP VIEW [ IF EXISTS ] <view_name>;
```

Views store a query definition. Keep names qualified when the current namespace
is not unambiguous. Use the published `ALTER VIEW` forms for view properties or
reflections rather than assuming table alterations apply to views.

## Functions

```sql
CREATE [ OR REPLACE ] FUNCTION [ IF NOT EXISTS ] <name>(<parameters>)
RETURNS { <data_type> | TABLE (<column_name> <data_type> [, ...]) }
RETURN { <expression> | <query> };
DROP FUNCTION [ IF EXISTS ] <function_name>;
```

UDFs may be scalar or tabular. A scalar UDF returns a single value and may use
an expression or query body. A tabular UDF declares `RETURNS TABLE (...)`, uses
a query body, and is called in the `FROM` clause through `TABLE(<udf>(...))`.
`OR REPLACE` and `IF NOT EXISTS` are mutually exclusive. Creating a UDF
requires documented catalog privileges; dropping one requires ownership. A UDF
body cannot contain DDL or DML statements.

```sql
CREATE FUNCTION add_tax(amount DECIMAL(12, 2))
RETURNS DECIMAL(12, 2)
RETURN amount * 1.20;
```

```sql
CREATE FUNCTION recent_orders()
RETURNS TABLE (order_id BIGINT, amount DECIMAL(12, 2))
RETURN SELECT order_id, amount FROM lakehouse.orders;

SELECT * FROM TABLE(recent_orders());
```

## Users and roles

Lifecycle syntax for principals is covered in
[CREATE USER](https://docs.dremio.com/dremio-cloud/sql/commands/create-user/),
[DROP USER](https://docs.dremio.com/dremio-cloud/sql/commands/drop-user/),
[CREATE ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/create-role/),
and [DROP ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/drop-role/).

```sql
CREATE USER "analyst@example.invalid";
DROP USER "analyst@example.invalid";
CREATE ROLE analysts;
DROP ROLE analysts;
```

Use quoted principal names where their characters require it. Deleting an
externally managed user does not prevent a later external sign-in from creating
a new account.
