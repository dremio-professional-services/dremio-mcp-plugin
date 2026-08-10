# Identifiers, keywords, and qualified names

Source: [Reserved keywords](https://docs.dremio.com/dremio-cloud/sql/keywords/).

## Reserved words

Dremio reserves ANSI keywords and additional words as part of its SQL grammar.
Do not use a reserved word unquoted as an object or column name. Quote it with
double quotes when it must be used as an identifier:

```sql
SELECT "select", "order"
FROM analytics."group";
```

Use the public keyword list as the authority rather than copying a partial list
into application code or assuming another SQL dialect has the same reservation
rules.

## Quoting and case

Use double quotes around identifiers containing spaces, punctuation, or reserved
words. String literals use single quotes and are not identifiers. The current
public reserved-keyword page documents quoting but does not establish general
identifier case-folding or case-sensitivity behavior; preserve the spelling and
case supplied by the catalog or request instead of inferring a broader rule.

```sql
SELECT "Order ID"
FROM Samples."example.dremio.com"."Orders 2025"
WHERE status = 'paid';
```

## Qualified paths

Use dot-separated namespace components to disambiguate an object. Quote each
component independently when necessary:

```sql
SELECT *
FROM lakehouse.sales.orders;

SELECT *
FROM Samples."example.dremio.com"."orders 2025";
```

Whether a path is valid also depends on its current source, catalog, namespace,
and privileges. Identifier syntax alone does not establish object availability.
