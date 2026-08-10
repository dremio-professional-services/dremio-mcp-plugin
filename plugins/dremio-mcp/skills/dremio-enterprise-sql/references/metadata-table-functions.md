# Metadata table functions

Source: [Enterprise table functions](https://docs.dremio.com/current/reference/sql/table-functions/).
Table functions are read-only `sys` functions returning tabular data for a
`FROM` clause. The dedicated system-table-function index lists the three
functions below. It is not an inventory of every public tabular or metadata
function: the [SELECT](https://docs.dremio.com/current/reference/sql/commands/SELECT-statements)
and [UDF](https://docs.dremio.com/current/reference/sql/commands/functions) references
may publish additional table or tabular functions, which this focused index does
not duplicate.

## `sys.recommend_reflections`

Source: [SYS.RECOMMEND_REFLECTIONS](https://docs.dremio.com/current/reference/sql/table-functions/recommend-reflections/).

```sql
SELECT * FROM TABLE(SYS.RECOMMEND_REFLECTIONS(ARRAY['00000000-0000-0000-0000-000000000000']))
```

Parameter: `ARRAY[...]`, an array literal of job-ID strings; at most 100 job
IDs, and the caller must be allowed to view every listed job. Returns
`view_sql varchar`, `reflection_sql varchar`, `job_ids list`,
`reflection_score double`, `average_improvement_factor double`, and
`average_improvement_ms double`. For a default raw Reflection recommendation,
`view_sql` is `--Default Raw Reflection`; `reflection_score` ranges from 0
(worst) to 100 (best). It cannot recommend Reflections for jobs with multiple
nested queries containing joins; only inner joins are supported (outer joins
within a view definition are supported), and window functions are not
supported.

## `sys.reflection_lineage`

Source: [SYS.REFLECTION_LINEAGE](https://docs.dremio.com/current/reference/sql/table-functions/reflection-lineage/).

```sql
SELECT * FROM TABLE(sys.reflection_lineage('00000000-0000-0000-0000-000000000000'))
```

Parameter: a Reflection ID `String`. Returns `batch_number integer`,
`reflection_id varchar`, `reflection_name varchar`, and `dataset_name varchar`.
A larger `batch_number` refreshes later; entries at the same depth refresh in
parallel.

## `sys.reflection_refresh_settings`

Source: [SYS.REFLECTION_REFRESH_SETTINGS](https://docs.dremio.com/current/reference/sql/table-functions/reflection-refresh-settings/).

```sql
SELECT * FROM TABLE(sys.reflection_refresh_settings('00000000-0000-0000-0000-000000000000'))
```

Parameter: a Reflection ID `String`. Returns `table_type varchar`,
`table_path varchar`, `table_version_context varchar`, `overrides_source boolean`,
`refresh_method varchar`, `refresh_policy varchar`,
`refresh_period_seconds double`, `refresh_schedule varchar`,
`never_expire boolean`, and `expire_after_seconds double`. Irrelevant numeric
fields use `-1`; irrelevant text fields use an empty string. The documented
schedule is a UTC cron expression.
