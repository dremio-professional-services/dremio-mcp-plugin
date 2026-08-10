# Enterprise 26.x data types, literals, and casts

Primary reference: https://docs.dremio.com/current/reference/sql/data-types/

## Supported families

| Family | Current documented types |
|---|---|
| Numeric | `INT`, `BIGINT`, `FLOAT`, `DOUBLE`, `DECIMAL` |
| String and binary | `VARCHAR`, `VARBINARY` |
| Boolean | `BOOLEAN` |
| Date and time | `DATE`, `TIME`, `TIMESTAMP`, `INTERVAL` |
| Semi-structured | `STRUCT`, `LIST`, `MAP` |

Use the linked page for ranges, precision, conversions, and source mappings.
Do not substitute similarly named types that the current table does not list.

## Literals and casts

```sql
DATE '2026-01-31'
TIME '17:30:50.235'
TIMESTAMP '2026-01-31 17:30:50.123'
INTERVAL '3' DAY
CAST(<expression> AS <type>)
```

The current page documents `yyyy-mm-dd` as the supported string-literal date
format, and the shown `TIME` formats. Timestamps have millisecond precision
without a time zone. For another input format, use the appropriate documented
conversion function rather than assuming an implicit cast.

`LIST` has `ARRAY[...]` literals; `STRUCT` has no STRUCT literal. STRUCT keys
and MAP keys are documented as case-insensitive strings, while ordinary SQL
identifier case behavior is covered separately.
