# Catalog namespaces and Nessie versioning

Current Nessie command index: https://docs.dremio.com/current/reference/sql/commands/nessie/

## Context and folders

Current context and folder pages: [USE](https://docs.dremio.com/current/reference/sql/commands/use/),
[CREATE FOLDER](https://docs.dremio.com/current/reference/sql/commands/nessie/create-folder/), and
[ALTER FOLDER](https://docs.dremio.com/current/reference/sql/commands/alter-folder/).

```sql
CREATE FOLDER [ IF NOT EXISTS ] <folder_name>
  [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT } <refValue> ];

ALTER FOLDER <folder_name>
  ROUTE REFLECTIONS TO { DEFAULT QUEUE | QUEUE { <queue_name> | <queue_uuid> } };
```

Use a qualified `<source>.<folder>` name to select a source; `CREATE FOLDER`
has no `IN <source_name>` clause. Without a source in the name, it uses the
query-context source. Its optional `AT` uses the current reference when absent.
`ALTER FOLDER` routes reflection create/refresh jobs and is not namespace
renaming or object metadata DDL.

## Branches and tags

```sql
CREATE BRANCH [ IF NOT EXISTS ] <branch_name>
  [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT } <refValue> ]
  [ IN <source_name> ];
CREATE TAG [ IF NOT EXISTS ] <tag_name>
  [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT } <refValue> ]
  [ IN <source_name> ];

ALTER BRANCH <branch_name>
  ASSIGN { REF[ERENCE] | BRANCH | TAG | COMMIT } <identifier>
  [ IN <source_name> ];
ALTER TAG <tag_name>
  ASSIGN { REF[ERENCE] | BRANCH | TAG | COMMIT } <identifier>
  [ IN <source_name> ];

DROP BRANCH [ IF EXISTS ] <branch_name>
  { AT COMMIT <commit_hash> | FORCE }
  [ IN <source_name> ];
DROP TAG [ IF EXISTS ] <tag_name>
  { AT COMMIT <commit_hash> | FORCE }
  [ IN <source_name> ];

MERGE BRANCH <source_branch_name>
  [ INTO <target_branch_name> ]
  [ IN <source_name> ];
SHOW BRANCHES [ IN <source_name> ];
SHOW TAGS [ IN <source_name> ];
SHOW LOG[S]
  [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT } <reference_name> ]
  [ IN <source_name> ];
```

Sources: [CREATE BRANCH](https://docs.dremio.com/current/reference/sql/commands/nessie/create-branch/),
[CREATE TAG](https://docs.dremio.com/current/reference/sql/commands/nessie/create-tag/),
[ALTER BRANCH](https://docs.dremio.com/current/reference/sql/commands/nessie/alter-branch/),
[ALTER TAG](https://docs.dremio.com/current/reference/sql/commands/nessie/alter-tag/),
[DROP BRANCH](https://docs.dremio.com/current/reference/sql/commands/nessie/drop-branch/),
[DROP TAG](https://docs.dremio.com/current/reference/sql/commands/nessie/drop-tag/), and
[MERGE BRANCH](https://docs.dremio.com/current/reference/sql/commands/nessie/merge-branch/),
[SHOW BRANCHES](https://docs.dremio.com/current/reference/sql/commands/nessie/show-branches/),
[SHOW TAGS](https://docs.dremio.com/current/reference/sql/commands/nessie/show-tags/), and
[SHOW LOGS](https://docs.dremio.com/current/reference/sql/commands/nessie/show-logs/).

Commit hashes in reference clauses must be double-quoted. `AT COMMIT` is the
compare-and-delete safeguard: it prevents a drop if the reference changed.
`FORCE` bypasses that safeguard. A merge without `INTO` targets the current
reference and succeeds only when that reference is a branch.

## VACUUM CATALOG

Source: https://docs.dremio.com/current/reference/sql/commands/nessie/vacuum-catalog/

```sql
VACUUM CATALOG <source_name>
  [ { INCLUDE | EXCLUDE }
    ( <table_name>
      [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT | SNAPSHOT | TIMESTAMP }
        <reference_name> ]
      [ AS OF <timestamp> ]
      [, <table_name>
        [ AT { REF[ERENCE] | BRANCH | TAG | COMMIT | SNAPSHOT | TIMESTAMP }
          <reference_name> ]
        [ AS OF <timestamp> ] ]* ) ];
```

It removes expired snapshots and orphaned metadata for all Iceberg tables in a
Nessie catalog source. Only catalog owners and `ADMIN` members may run it, and
the listed cleanup prerequisites must be completed first. `INCLUDE` and
`EXCLUDE` are mutually exclusive. A reference identifies the table but an
exclusion applies across all its branches, commits, and references. `AS OF` is
for Iceberg table queries and requires a SQL expression that resolves to one
TIMESTAMP value.
