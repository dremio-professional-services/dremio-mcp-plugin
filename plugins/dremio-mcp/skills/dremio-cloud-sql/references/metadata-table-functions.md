# Metadata table functions

Source: [Cloud table functions](https://docs.dremio.com/dremio-cloud/sql/table-functions/).
Table functions return tabular data for use in `FROM`; all are in `sys` and are
read-only.

## `SYS.RECOMMEND_REFLECTIONS`

Source: [SYS.RECOMMEND_REFLECTIONS](https://docs.dremio.com/dremio-cloud/sql/table-functions/recommend-reflections/).

```sql
SELECT *
FROM TABLE(SYS.RECOMMEND_REFLECTIONS(ARRAY['<jobId>', '<jobId>']));
```

The parameter is the documented array literal of job-ID strings. It accepts up
to 100 job IDs, and the user must be allowed to view every listed job. It
returns `view_sql varchar`, `reflection_sql varchar`, `job_ids list`,
`reflection_score double`, `average_improvement_factor double`, and
`average_improvement_ms double`.

Limitations: it cannot recommend Reflections for jobs with multiple nested
queries that contain joins; the query can contain only inner joins (outer joins
inside a view definition are supported); and the query cannot contain window
functions.

## `sys.reflection_lineage`

Source: [SYS.REFLECTION_LINEAGE](https://docs.dremio.com/dremio-cloud/sql/table-functions/reflection-lineage/).

```sql
SELECT *
FROM TABLE(sys.reflection_lineage('<reflection_id_or_name>'));
```

`<reflection_id_or_name>` is a `String` Reflection ID or name. The function
returns `batch_number integer`, `reflection_id varchar`,
`reflection_name varchar`, and `dataset_name varchar`. `batch_number` describes
the dependency-graph depth; a larger value refreshes later, while entries at
the same value refresh in parallel.

## `sys.reflection_refresh_settings`

Source: [SYS.REFLECTION_REFRESH_SETTINGS](https://docs.dremio.com/dremio-cloud/sql/table-functions/reflection-refresh-settings/).

```sql
SELECT *
FROM TABLE(sys.reflection_refresh_settings('<reflection_id_or_name>'));
```

`<reflection_id_or_name>` is a `String` Reflection ID or name. The function
returns `table_type varchar`, `table_path varchar`, `table_version_context
varchar`, `overrides_source boolean`, `refresh_method varchar`,
`refresh_policy varchar`, `refresh_period_seconds double`,
`refresh_schedule varchar`, `never_expire boolean`, and
`expire_after_seconds double`. Irrelevant numeric fields use `-1`; irrelevant
text fields use an empty string.
