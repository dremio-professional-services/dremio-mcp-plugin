# Catalogs, folders, spaces, and qualified names

Sources: [CREATE FOLDER](https://docs.dremio.com/dremio-cloud/sql/commands/create-folder/),
[DROP FOLDER](https://docs.dremio.com/dremio-cloud/sql/commands/drop-folder/),
[CREATE SPACE](https://docs.dremio.com/dremio-cloud/sql/commands/create-space/),
[ALTER SPACE](https://docs.dremio.com/dremio-cloud/sql/commands/alter-space/),
[DROP SPACE](https://docs.dremio.com/dremio-cloud/sql/commands/drop-space/),
[ALTER SOURCE](https://docs.dremio.com/dremio-cloud/sql/commands/alter-source/),
and the [SQL command index](https://docs.dremio.com/dremio-cloud/sql/commands/).

## Namespace lifecycle

```sql
CREATE FOLDER <folder_name>;
DROP FOLDER <folder_name>;
CREATE SPACE <space_name>;
ALTER SPACE <space_name> <alteration>;
DROP SPACE <space_name>;
ALTER SOURCE <source_name> <alteration>;
```

Use the individual command pages for the permitted options and required
privileges. A source is an external data connection, while a space and folder
organize objects. Do not assume that an operation supported by a catalog applies
to every source type.

## Qualified objects

Object names can include a namespace path. Quote each component that has spaces,
punctuation, or a reserved word. For example:

```sql
SELECT order_id
FROM lakehouse.sales.orders;

SELECT order_id
FROM Samples."example.dremio.com"."orders 2025";
```

Qualification matters whenever the object is not in the current context. Create
the containing namespace before creating a table or view inside it. Names and
the exact available namespace operations are source- and privilege-dependent.

## Scope boundary

This reference covers the publicly indexed Cloud commands above. It does not
introduce catalog branch or tag-reference commands.
