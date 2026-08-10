# Apache Iceberg maintenance and pipes

Current Iceberg command index: https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/

## Maintenance

Sources: [OPTIMIZE](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/optimize-table/),
[ROLLBACK](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/rollback-table/), and
[VACUUM](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/vacuum-table/).

```sql
OPTIMIZE TABLE <table_name>
  [ REWRITE DATA [ USING BIN_PACK ]
    [ ( { TARGET_FILE_SIZE_MB | MIN_FILE_SIZE_MB | MAX_FILE_SIZE_MB | MIN_INPUT_FILES }
      = <value> [, ... ] ) ]
    [ FOR PARTITIONS <predicate> ] ]
  [ REWRITE MANIFESTS ];

ROLLBACK TABLE <table_name>
  TO { SNAPSHOT '<snapshot_id>' | TIMESTAMP '<timestamp>' };

VACUUM TABLE <table_name>
  { EXPIRE SNAPSHOTS [ older_than = <value> ] [ retain_last = <value> ]
  | REMOVE ORPHAN FILES [ older_than = <value> ] [ location = <value> ] };
```

`OPTIMIZE TABLE` rewrites data and manifest files of an Apache Iceberg table.
It requires membership in `ADMIN`, table ownership, or both `SELECT` and
`UPDATE` privileges on the table. Omitted clauses use `REWRITE DATA`; `USING
BIN_PACK` is optional because it is the only documented strategy. The data
rewrite options apply to partitioned tables; `FOR PARTITIONS` applies only to
`REWRITE DATA`. `REWRITE MANIFESTS` cannot be combined with `REWRITE DATA`.
The command rewrites files and can consume substantial compute, so validate
the table, partition predicate, and scheduling window first.

```sql
OPTIMIZE TABLE <table_name>
  REWRITE DATA USING BIN_PACK (TARGET_FILE_SIZE_MB = 512, MIN_INPUT_FILES = 10);
```

`VACUUM TABLE` requires exactly one operation: `EXPIRE SNAPSHOTS` or `REMOVE
ORPHAN FILES`; a bare `VACUUM TABLE` is not valid. It requires table
`OWNERSHIP` or membership in the `ADMIN` role. `EXPIRE SNAPSHOTS` defaults
`older_than` to five days before execution and accepts only UTC timestamps.
`REMOVE ORPHAN FILES` defaults `older_than` to three days before execution
when omitted or lower, and defaults `location` to the table root. Its `location`
must be a subdirectory of the table root and is unsupported for HDFS tables;
missing HDFS access also prevents orphan-file removal. Both forms permanently
remove data or metadata, so verify recovery and retention requirements first.

## Standalone `COPY INTO`

Sources: [COPY INTO](https://docs.dremio.com/current/reference/sql/commands/apache-iceberg-tables/copy-into-table/)
and [Copying Data Into Apache Iceberg Tables](https://docs.dremio.com/current/developer/data-formats/apache-iceberg/copying-data-into-tables/).

```sql
COPY INTO <table_name>
  [ AT { REF[ERENCE] | BRANCH } <reference_name> ]
  FROM '@<storage_location_name>[/<path>[/<file_name>]]'
  [ FILES ( '<file_name>' [, ...] ) | REGEX '<regex_pattern>' ]
  [ FILE_FORMAT { 'csv' | 'json' | 'parquet' } ]
  [ ( { <csv_options> | <json_options> | <parquet_options> } ) ];

COPY INTO <table_name>
  FROM ( SELECT [ $<file_column_number> | <file_column_name> ] [, ...]
    FROM '@<storage_location_name>[/<path>[/<file_name>]]' )
  [ FILES ( '<file_name>' [, ...] ) | REGEX '<regex_pattern>' ]
  [ FILE_FORMAT { 'csv' | 'parquet' } ]
  [ ( { <csv_options> | <parquet_options> } ) ];
```

The target must be an existing Iceberg table in an AWS Glue Data Catalog, Hive
Metastore, or Nessie Catalog. The source must be a preconfigured Dremio source
on Azure Storage, Google Cloud Storage, HDFS, NAS, or Amazon S3. `AT` applies
only to Nessie catalogs. At least one target column must match a column in every
data file; duplicate source-column names cause an error, and CSV files require
a header.

`FILES` and `REGEX` are mutually exclusive; either is also mutually exclusive
with a file name in the source path. A list has at most 1,000 files. `FILE_FORMAT`
is optional only when an extension determines it, and all input files must share
one format. The transformation form supports only CSV and Parquet; it selects
source-file columns and does not add the Nessie `AT` clause shown by the
standalone data-load form.

`csv_options` are `DATE_FORMAT`, `EMPTY_AS_NULL`, `ESCAPE_CHAR`,
`EXTRACT_HEADER`, `FIELD_DELIMITER`, `NULL_IF`, `ON_ERROR`, `QUOTE_CHAR`,
`RECORD_DELIMITER`, `SKIP_LINES`, `TIME_FORMAT`, `TIMESTAMP_FORMAT`, and
`TRIM_SPACE`. `json_options` are the applicable date/null/error/time/timestamp/
trim options. For CSV and JSON, `ON_ERROR` accepts `'abort'`, `'continue'`, or
`'skip_file'`; `'abort'` is the default. For Parquet, only `ON_ERROR` is
supported and it accepts `'abort'` or `'skip_file'`. `continue` can load valid
CSV rows while rejecting bad ones; `skip_file` rejects a file at its first
error and has extra processing cost.

```sql
COPY INTO <table_name>
  FROM '@<storage_location_name>/<path>/'
  FILE_FORMAT 'json';
```

## Autoingest pipe lifecycle

Sources: [CREATE PIPE](https://docs.dremio.com/current/reference/sql/commands/create-pipe/),
[ALTER PIPE](https://docs.dremio.com/current/reference/sql/commands/alter-pipe/),
[DESCRIBE PIPE](https://docs.dremio.com/current/reference/sql/commands/describe-pipe/), and
[DROP PIPE](https://docs.dremio.com/current/reference/sql/commands/drop-pipe/).

```sql
CREATE PIPE [ IF NOT EXISTS ] <pipe_name>
  [ DEDUPE_LOOKBACK_PERIOD <number_of_days> ]
  NOTIFICATION_PROVIDER <notification_provider>
  NOTIFICATION_QUEUE_REFERENCE <notification_queue_ref>
  AS COPY INTO <table_name>
    [ AT BRANCH <branch_name> ]
    FROM '@<storage_location_name>'
    FILE_FORMAT { 'csv' | 'json' | 'parquet' }
    [ ( { <csv_format_options> | <json_format_options> | <parquet_format_options> } ) ];

ALTER PIPE <pipe_name>
  { SET PIPE_EXECUTION_RUNNING = { TRUE | FALSE }
  | [ DEDUPE_LOOKBACK_PERIOD <number_of_days> ]
    AS COPY INTO <table_name>
      [ AT BRANCH <branch_name> ]
      FROM '@<storage_location_name>'
      FILE_FORMAT { 'csv' | 'json' | 'parquet' }
      [ ( { <csv_format_options> | <json_format_options> | <parquet_format_options> } ) ] };

DESCRIBE PIPE <pipe_name>;
DROP PIPE <pipe_name>;
```

For CSV, the current named option production permits `DATE_FORMAT`,
`EMPTY_AS_NULL`, `ESCAPE_CHAR`, `EXTRACT_HEADER`, `FIELD_DELIMITER`, `NULL_IF`,
`ON_ERROR 'skip_file'`, `QUOTE_CHAR`, `RECORD_DELIMITER`, `SKIP_LINES`,
`TIME_FORMAT`, `TIMESTAMP_FORMAT`, and `TRIM_SPACE`. JSON supports the
applicable date/null/error/time/timestamp/trim options; Parquet supports only
`ON_ERROR 'skip_file'`. `ON_ERROR 'skip_file'` is the default and the only
supported pipe error option.

Pipes only apply to Apache Iceberg tables and can ingest only Amazon S3 sources
in current Enterprise documentation. For S3, the documented provider is
`AWS_SQS`; the notification queue reference identifies the event queue.
`FILE_FORMAT` is required and all loaded files must share it. The target branch
defaults to `main` when omitted; ALTER PIPE cannot modify the target branch or
the target table. The pipe name and the `@<storage_location_name>` source name
cannot be modified. `DEDUPE_LOOKBACK_PERIOD` defaults to `14`, accepts `0` to `90` days, and `0`
disables file deduplication. A positive dedupe period treats
same-name files written inside that period as duplicates even after deletion and
re-upload.

The pipe-embedded `COPY INTO` grammar above is distinct from standalone `COPY
INTO`: it is restricted to pipe-supported S3 ingestion with `AWS_SQS` and only
documents `ON_ERROR 'skip_file'`.
