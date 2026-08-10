# Aggregate, window, and percentile functions

Cloud SQL functions in the Aggregate, Window, and Percentile categories. A function can be used as a window function only where its documented `OVER` form applies.

## Aggregate

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| APPROX_COUNT_DISTINCT | `APPROX_COUNT_DISTINCT(column_name ANY PRIMITIVE) -> BIGINT`; approximate unique non-null count. | Column may be any primitive type. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/APPROX_COUNT_DISTINCT/) |
| ARRAY_AGG | `ARRAY_AGG([DISTINCT] expression) -> ARRAY`; aggregates primitive values to an array. | `DISTINCT` is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_AGG/) |
| ARRAY_AVG | `ARRAY_AVG(list_column LIST) -> NUMERIC`; average of list elements. | List must be a column, not an array literal, with numeric elements. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_AVG/) |
| ARRAY_MAX | `ARRAY_MAX(list_column LIST) -> NUMERIC`; largest list element. | List must be a column, not an array literal, with numeric elements. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_MAX/) |
| ARRAY_MIN | `ARRAY_MIN(list_column LIST) -> NUMERIC`; smallest list element. | List must be a column, not an array literal, with numeric elements. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_MIN/) |
| ARRAY_SUM | `ARRAY_SUM(list_column LIST) -> NUMERIC`; sum of list elements. | List must be a column, not an array literal, with numeric elements. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_SUM/) |
| AVG | `AVG(numeric_expression NUMERIC) -> DOUBLE`; average. | Accepts double, numeric, integer, `INTERVAL_DATE`, or `INTERVAL_YEAR`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/AVG/) |
| BIT_AND | `BIT_AND(expression INT) -> INT`; aggregate bitwise AND. | Input must be castable to integer. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BIT_AND/) |
| BIT_OR | `BIT_OR(expression INT) -> INT`; aggregate bitwise OR. | Input must be castable to integer. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BIT_OR/) |
| CORR | `CORR(expression1 NUMERIC, expression2 NUMERIC) -> DOUBLE`; Pearson correlation. | The function name must be double-quoted. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CORR/) |
| COUNT | `COUNT(expression ANY) -> BIGINT`; record count. | `*` includes rows with `NULL`; a column expression excludes them. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COUNT/) |
| COVAR_POP | `COVAR_POP(expression1 NUMERIC, expression2 NUMERIC) -> DOUBLE`; population covariance. | Both expressions are numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COVAR_POP/) |
| COVAR_SAMP | `COVAR_SAMP(expression1 NUMERIC, expression2 NUMERIC) -> DOUBLE`; sample covariance. | Both expressions are numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COVAR_SAMP/) |
| LISTAGG | `LISTAGG([ALL or DISTINCT] measure_expr [, 'delimiter']) [WITHIN GROUP (ORDER BY measure_expr [ASC or DESC])]`; concatenated string list. | `ALL` is default; `DISTINCT` removes duplicates. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LISTAGG/) |
| MAX | `MAX(expression NUMERIC) -> NUMERIC`; maximum. | Evaluates across rows. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MAX/) |
| MEDIAN | `MEDIAN(num_col NUMERIC) -> DOUBLE PRECISION`; continuous-distribution median. | Input is a numeric column. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MEDIAN/) |
| MIN | `MIN(expression NUMERIC) -> NUMERIC`; minimum. | Evaluates across rows. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MIN/) |
| NDV | `NDV(expression NUMERIC [, scale NUMERIC]) -> BIGINT`; approximate distinct count. | Scale is an integer from 1 through 10. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/NDV/) |
| STDDEV | `STDDEV(col_name NUMERIC) -> DOUBLE`; standard deviation. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV/) |
| STDDEV_POP | `STDDEV_POP(col_name NUMERIC) -> DOUBLE`; population standard deviation. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV_POP/) |
| STDDEV_SAMP | `STDDEV_SAMP(col_name NUMERIC) -> DOUBLE`; sample standard deviation. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV_SAMP/) |
| SUM | `SUM(col_name NUMERIC) -> input type, except INT -> BIGINT`; sum. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SUM/) |
| VAR_POP | `VAR_POP(col_name NUMERIC) -> NUMERIC`; population variance. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/VAR_POP/) |
| VAR_SAMP | `VAR_SAMP(col_name NUMERIC) -> NUMERIC`; sample variance. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/VAR_SAMP/) |

## Window

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| AVG, COUNT, COVAR_POP, COVAR_SAMP, MAX, MIN, STDDEV_POP, SUM, VAR_POP | Use their documented aggregate signatures with `OVER`; each returns its normal documented type. | These pages document cumulative-window support; partitioning, ordering, and frame follow the documented window syntax. | [AVG](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/AVG/), [COUNT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COUNT/), [COVAR_POP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COVAR_POP/), [COVAR_SAMP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COVAR_SAMP/), [MAX](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MAX/), [MIN](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MIN/), [STDDEV_POP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV_POP/), [SUM](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SUM/), [VAR_POP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/VAR_POP/) |
| STDDEV_SAMP, VAR_SAMP | Use their documented aggregate signatures with `OVER`; return their normal documented type. | Their pages specifically document sliding-window frame support. | [STDDEV_SAMP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV_SAMP/), [VAR_SAMP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/VAR_SAMP/) |
| NDV | `NDV(expression NUMERIC [, scale NUMERIC]) -> BIGINT`; approximate distinct count. | It is cross-listed in Window but its detail page does not document an `OVER` form. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/NDV/) |
| CUME_DIST | `CUME_DIST() OVER ([PARTITION BY partition_expression] ORDER BY order_expression) -> DOUBLE`; cumulative distribution. | `ORDER BY` is required; `PARTITION BY` is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CUME_DIST/) |
| DENSE_RANK | `DENSE_RANK() OVER ([PARTITION BY partition_expression] ORDER BY order_expression) -> BIGINT`; rank without gaps. | `ORDER BY` is required; `PARTITION BY` is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/DENSE_RANK/) |
| FIRST_VALUE | `FIRST_VALUE(expression) OVER ([PARTITION BY expressionlist] [ORDER BY fieldlist] [cumulativeFrame \| slidingFrame])`; first value in the window. | `PARTITION BY`, `ORDER BY`, and a frame are optional; `ORDER BY` is required when a cumulative or sliding frame is used. | [FIRST_VALUE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/FIRST_VALUE/), [window syntax](https://docs.dremio.com/dremio-cloud/sql/sql-functions/WINDOW/) |
| LAG | `LAG(expression [, offset]) OVER ([PARTITION BY partition_expression] [ORDER BY order_expression]) -> same as input`; prior value. | Offset is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LAG/) |
| LAST_VALUE | `LAST_VALUE(expression) OVER ([PARTITION BY expressionlist] [ORDER BY fieldlist] [cumulativeFrame \| slidingFrame])`; last value in the window. | `PARTITION BY`, `ORDER BY`, and a frame are optional; `ORDER BY` is required when a cumulative or sliding frame is used. | [LAST_VALUE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LAST_VALUE/), [window syntax](https://docs.dremio.com/dremio-cloud/sql/sql-functions/WINDOW/) |
| LEAD | `LEAD(expression [, offset]) OVER ([PARTITION BY partition_expression] [ORDER BY order_expression]) -> same as input`; following value. | Offset is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LEAD/) |
| NTILE | `NTILE(buckets) OVER ([PARTITION BY partition_expression] ORDER BY order_expression) -> INT`; bucket number. | `buckets` is a positive integer literal; `PARTITION BY` is optional and `ORDER BY` is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/NTILE/) |
| PERCENT_RANK | `PERCENT_RANK() OVER ([PARTITION BY partition_expression] ORDER BY order_expression) -> DOUBLE`; relative rank. | `ORDER BY` is required; `PARTITION BY` is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/PERCENT_RANK/) |
| RANK | `RANK() OVER ([PARTITION BY partition_expression] ORDER BY order_expression) -> BIGINT`; rank with gaps. | `ORDER BY` is required; `PARTITION BY` is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/RANK/) |
| ROW_NUMBER | `ROW_NUMBER() OVER ([PARTITION BY partition_expression] [ORDER BY order_expression]) -> BIGINT`; row ordinal. | Ordering is optional in the documented syntax. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ROW_NUMBER/) |

```sql
SELECT SUM(amount) OVER (PARTITION BY account_id ORDER BY order_date)
FROM orders;
```

## Percentile

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| APPROX_PERCENTILE | `APPROX_PERCENTILE(column_name NUMERIC, percentile DOUBLE) -> DOUBLE`; approximate percentile. | Percentile must be from 0 through 1. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/APPROX_PERCENTILE/) |
| MEDIAN | `MEDIAN(num_col NUMERIC) -> DOUBLE PRECISION`; continuous median. | Input is numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MEDIAN/) |
| PERCENTILE_CONT | `PERCENTILE_CONT(fraction DOUBLE PRECISION) WITHIN GROUP (ORDER BY order_by_expression NUMERIC [ASC or DESC]) -> DOUBLE PRECISION`; continuous percentile. | Fraction is a numeric literal from 0 through 1; exactly one `ORDER BY` expression. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/PERCENTILE_CONT/) |
| PERCENTILE_DISC | `PERCENTILE_DISC(fraction DOUBLE PRECISION) WITHIN GROUP (ORDER BY order_by_expression [ASC or DESC]) -> DOUBLE PRECISION`; discrete percentile. | Fraction is a numeric literal from 0 through 1; exactly one `ORDER BY` expression. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/PERCENTILE_DISC/) |
