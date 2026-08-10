# Data types, literals, and casts

Source: [Dremio Cloud data types](https://docs.dremio.com/dremio-cloud/sql/data-types/).

## Scalar types

The public reference documents numeric types `INT`, `BIGINT`, `FLOAT`,
`DOUBLE`, and `DECIMAL(p, s)`; text and binary types `VARCHAR` and `VARBINARY`;
logical `BOOLEAN`; and temporal `DATE`,
`TIME`, `TIMESTAMP[(precision)]`, and `INTERVAL`.

Use typed literals where they remove ambiguity:

```sql
SELECT DATE '2025-01-31',
       TIME '17:30:50.235',
       TIMESTAMP '2025-01-31 17:30:50.123456',
       INTERVAL '3' DAY,
       CAST('42.50' AS DECIMAL(12, 2));
```

`VARCHAR` is UTF-8 text. `VARBINARY` is variable-length binary data. Boolean
literals are `TRUE`, `FALSE`, and `NULL`. Timestamp precision differs by
Iceberg table version; specify precision in DDL, not in a timestamp literal.

## Complex and semi-structured types

`ARRAY`, `STRUCT`, and `MAP` model nested values. Map keys must be strings;
map values can be numbers, booleans, or strings (but not `NULL`).

```sql
SELECT ARRAY['new', 'paid'];
SELECT CONVERT_FROM('{"name":"Ada","active":true}', 'json');
SELECT attributes['region'] FROM lakehouse.events;
```

`VARIANT` stores self-describing semi-structured values. It is available only
for Apache Iceberg v3 tables; use it for flexible, schema-on-read data rather
than assuming it works on every table type.

## UUID availability

`UUID` is a 16-byte identifier type supported only for Apache Iceberg tables.
It does not enforce uniqueness. UUID values are case-insensitive; an invalid
string or incorrectly sized binary cast raises an error.

```sql
CREATE TABLE lakehouse.users (user_id UUID, name VARCHAR);
SELECT UUID '619fbd6f-5114-40c7-a83f-1f0e114adae2';
```

## Cast discipline

Use `CAST(<expression> AS <type>)` when a conversion is documented and desired.
Validate inputs before relying on a conversion: values outside a type's range,
invalid temporal or UUID text, and incompatible complex shapes can fail. Check
the source page for implicit conversion and COPY INTO behavior.
