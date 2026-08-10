# Identifiers and reserved words

Reserved-word reference: https://docs.dremio.com/current/reference/sql/reserved-keywords

## Quoting and qualified names

Use dot-qualified names such as `<source>.<path>.<object>` where the object
context is not otherwise selected. Enclose a reserved word used as an object
name in double quotes:

```sql
SELECT * FROM source.folder."boolean";
```

The current page states that Dremio reserves ANSI and additional keywords, and
explicitly permits a reserved keyword as an object name when double-quoted.
Consult that page for the complete current list rather than embedding a stale
copy here.

## Case boundary

The current reserved-word page does not state a general case-folding rule for
ordinary SQL identifiers. Therefore do not claim one from this skill. Preserve
the spelling and quoting supplied by the catalog, and use double quotes when a
name is reserved or contains characters requiring quoting. The documented
case-insensitivity of STRUCT and MAP keys does not establish a rule for SQL
identifiers.
