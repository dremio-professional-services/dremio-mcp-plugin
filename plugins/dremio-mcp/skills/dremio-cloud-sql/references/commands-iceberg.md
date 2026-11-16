# Iceberg tables and maintenance

Sources: [COPY INTO](https://docs.dremio.com/dremio-cloud/sql/commands/copy-into-table/),
[ANALYZE TABLE](https://docs.dremio.com/dremio-cloud/sql/commands/analyze-table/),
[OPTIMIZE TABLE](https://docs.dremio.com/dremio-cloud/sql/commands/optimize-table/),
[ROLLBACK TABLE](https://docs.dremio.com/dremio-cloud/sql/commands/rollback-table/),
[VACUUM TABLE](https://docs.dremio.com/dremio-cloud/sql/commands/vacuum-table/),
[SHOW TBLPROPERTIES](https://docs.dremio.com/dremio-cloud/sql/commands/show-table-properties/),
and [SELECT](https://docs.dremio.com/dremio-cloud/sql/commands/SELECT/).

## Preconditions

These operations are not interchangeable for arbitrary tables. `COPY INTO`
loads an existing Apache Iceberg table. `OPTIMIZE`, `ROLLBACK`, and `VACUUM`
are Iceberg maintenance operations that require a compatible Iceberg table and
the documented privileges. The snapshot and timestamp `SELECT` time-travel
forms also apply to compatible Delta Lake tables; that query support does not
broaden these Iceberg-only maintenance commands. Check the command page before
an operation that rewrites data or deletes historical files.

## COPY INTO

```sql
COPY INTO <table_name>
FROM '@<storage_location>[/<path>[/<file_name>]]'
[ FILES ('<file_name>' [, ...]) | REGEX '<pattern>' ]
[ FILE_FORMAT 'csv' | 'json' | 'parquet' ]
[ (<format_options>) ];
```

The storage location must be a preconfigured source. `FILES` and `REGEX` are
mutually exclusive; so are either of them and an explicit filename in `FROM`.
All files in one load have the same format. CSV and JSON support documented
format and error-handling options; Parquet supports only its documented options.

```sql
COPY INTO lakehouse.orders
FROM '@landing/incoming/orders/'
FILE_FORMAT 'csv'
(EXTRACT_HEADER 'true', ON_ERROR 'abort');
```

## Statistics and physical maintenance

```sql
ANALYZE TABLE <table_name>
  FOR { ALL COLUMNS | COLUMNS (<column_name> [, ...]) }
  { COMPUTE | DELETE } STATISTICS;

OPTIMIZE TABLE <table_name> [ FOR PARTITIONS <predicate> ];
```

`ANALYZE TABLE` computes or removes column statistics. `OPTIMIZE TABLE`
rewrites data and manifest files; the optional partition form is documented as
available but planned for deprecation. Do not assume an optimization finishes in
one pass for clustered data.

```sql
SHOW TBLPROPERTIES <table_name>;
```

`SHOW TBLPROPERTIES` returns `table_property_name`, `table_property_value`,
and `table_property_source` for an Iceberg table. The source is `TABLE` for a
value set on the table or `SYSTEM` for a system-option value; `SYSTEM` rows
appear only when that value differs from the Iceberg default.

## Snapshot recovery and cleanup

```sql
ROLLBACK TABLE <table_name>
TO { SNAPSHOT '<snapshot_id>' | TIMESTAMP '<utc_timestamp>' };

VACUUM TABLE <table_name>
{ EXPIRE SNAPSHOTS [ older_than = '<utc_timestamp>' ] [ retain_last = <count> ]
| REMOVE ORPHAN FILES [ older_than = '<utc_timestamp>' ] [ location = '<path>' ] };
```

Rollback selects a previous snapshot by ID or UTC timestamp. `VACUUM` destroys
eligible snapshots or orphan files; review retention, location, and URI-scheme
limitations before running it. Time-travel reads use the documented
`SELECT ... AT SNAPSHOT` or `SELECT ... AT <timestamp>` forms for compatible
Iceberg and Delta Lake tables in [SELECT](https://docs.dremio.com/dremio-cloud/sql/commands/SELECT/).
