# Semi-structured, UUID, and variant functions

Cloud SQL functions in the Semi-Structured Data, UUID Type, and Variant Type categories. Arrays, UUIDs, and variants remain separate value domains even when their predicate functions share a common `BOOLEAN` result.

## Arrays and maps

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| ARRAYS_OVERLAP | `ARRAYS_OVERLAP(array1, array2) -> BOOLEAN`; common-element test. | Both arguments are arrays. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAYS_OVERLAP/) |
| ARRAY_AGG | `ARRAY_AGG([DISTINCT] expression) -> ARRAY`; aggregate array. | Expression is primitive; `DISTINCT` is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_AGG/) |
| ARRAY_APPEND | `ARRAY_APPEND(array, value) -> ARRAY`; appends an element. | Array and value are required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_APPEND/) |
| ARRAY_AVG | `ARRAY_AVG(list_column LIST) -> NUMERIC`; average of list values. | Numeric list column, not an array literal. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_AVG/) |
| ARRAY_CAT | `ARRAY_CAT(array1, array2) -> ARRAY`; concatenated arrays. | Both arguments are arrays. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_CAT/) |
| ARRAY_COMPACT | `ARRAY_COMPACT(array) -> ARRAY`; removes null entries. | Input is an array. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_COMPACT/) |
| ARRAY_CONTAINS | `ARRAY_CONTAINS(array, value) -> BOOLEAN`; element-membership test. | Input is an array. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_CONTAINS/) |
| ARRAY_DISTINCT | `ARRAY_DISTINCT(array) -> ARRAY`; de-duplicated array. | Input is an array. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_DISTINCT/) |
| ARRAY_FREQUENCY | `ARRAY_FREQUENCY(array) -> MAP`; element frequencies. | Input is an array. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_FREQUENCY/) |
| ARRAY_GENERATE_RANGE | `ARRAY_GENERATE_RANGE(start, end [, step]) -> ARRAY`; integer sequence. | Step is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_GENERATE_RANGE/) |
| ARRAY_INSERT | `ARRAY_INSERT(array, position, value) -> ARRAY`; inserts an element. | Position is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_INSERT/) |
| ARRAY_MAX, ARRAY_MIN, ARRAY_SUM | `ARRAY_MAX(list_column LIST)`, `ARRAY_MIN(list_column LIST)`, `ARRAY_SUM(list_column LIST) -> NUMERIC`; numeric-list aggregate values. | Each requires a numeric list column, not an array literal. | [MAX](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_MAX/), [MIN](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_MIN/), [SUM](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_SUM/) |
| ARRAY_POSITION | `ARRAY_POSITION(element ANY, arr LIST) -> numeric`; index of the first matching element. | `element` is searched in `arr`; returns `NULL` when no match is found. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_POSITION/) |
| ARRAY_PREPEND | `ARRAY_PREPEND(value, array) -> ARRAY`; prepends an element. | Array and value are required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_PREPEND/) |
| ARRAY_REMOVE | `ARRAY_REMOVE(array, value) -> ARRAY`; removes matching elements. | Input is an array. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_REMOVE/) |
| ARRAY_REMOVE_AT | `ARRAY_REMOVE_AT(array, position) -> ARRAY`; removes at position. | Position is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_REMOVE_AT/) |
| ARRAY_SIZE | `ARRAY_SIZE(array) -> INTEGER`; array length. | Input is an array. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_SIZE/) |
| ARRAY_SLICE | `ARRAY_SLICE(arr LIST, from INT, to INT) -> LIST`; array section. | The syntax and parameter list require all three arguments and make `to` exclusive; the rendered examples omit `from` and `to` even though their captions supply both values. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_SLICE/) |
| ARRAY_TO_STRING | `ARRAY_TO_STRING(list, delimiter) -> VARCHAR`; list serialization. | Delimiter is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_TO_STRING/) |
| CARDINALITY | `CARDINALITY(collection) -> INTEGER`; collection size. | Input is a collection. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CARDINALITY/) |
| FLATTEN | `FLATTEN(array) -> rows`; expands array elements. | Use as documented in a query projection. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/FLATTEN/) |
| MAP_KEYS | `MAP_KEYS(map) -> ARRAY`; map keys. | Input is a map. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MAP_KEYS/) |
| MAP_VALUES | `MAP_VALUES(map) -> ARRAY`; map values. | Input is a map. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MAP_VALUES/) |
| SET_UNION | `SET_UNION(array1, array2) -> ARRAY`; union of array values. | Both arguments are arrays. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SET_UNION/) |
| SUBLIST | `SUBLIST(arr LIST, offset INT, length INT) -> LIST`; list subsection. | All three arguments are required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SUBLIST/) |

## UUID and variant values

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| GENERATE_UUID | `GENERATE_UUID() -> UUID`; generated UUID. | No arguments. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/GENERATE_UUID/) |
| IS_UUID | `IS_UUID(value VARIANT) -> BOOLEAN`; UUID type test. | Input must be `VARIANT`; tests for `VARIANT<UUID>`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_UUID/) |
| IS_BIGINT, IS_INT, IS_VARCHAR | `IS_BIGINT(expression ANY) -> BOOLEAN`; `IS_INT(expression ANY) -> BOOLEAN`; `IS_VARCHAR(expression ANY) -> BOOLEAN`. | These three predicates accept any input. | [IS_BIGINT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_BIGINT/), [IS_INT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_INT/), [IS_VARCHAR](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_VARCHAR/) |
| IS_BOOLEAN, IS_DATE, IS_DECIMAL, IS_DOUBLE, IS_FLOAT, IS_LIST, IS_STRUCT, IS_TIMESTAMP, IS_TIME, IS_VARBINARY | `IS_type(value VARIANT) -> BOOLEAN`; tests the named VARIANT type. | These predicates require `VARIANT` input. | [IS_BOOLEAN](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_BOOLEAN/), [IS_DATE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_DATE/), [IS_DECIMAL](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_DECIMAL/), [IS_DOUBLE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_DOUBLE/), [IS_FLOAT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_FLOAT/), [IS_LIST](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_LIST/), [IS_STRUCT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_STRUCT/), [IS_TIMESTAMP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_TIMESTAMP/), [IS_TIME](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_TIME/), [IS_VARBINARY](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_VARBINARY/) |
| IS_VARIANT_NULL | `IS_VARIANT_NULL(variant VARIANT) -> BOOLEAN`; tests a `VARIANT<NULL>` value. | A variant null is distinct from SQL `NULL`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_VARIANT_NULL/) |
| PARSE_JSON | `PARSE_JSON(string) -> VARIANT`; parses JSON. | Input must be JSON text. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/PARSE_JSON/) |
| TO_JSON | `TO_JSON(variant) -> VARCHAR`; serializes a variant to JSON. | Input is a variant. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_JSON/) |
| TO_VARIANT | `TO_VARIANT(expression) -> VARIANT`; converts to variant. | Input expression is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_VARIANT/) |
| TRY_PARSE_JSON | `TRY_PARSE_JSON(string) -> VARIANT or NULL`; non-throwing JSON parse. | Invalid JSON yields null. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TRY_PARSE_JSON/) |
| TRY_VARIANT_GET | `TRY_VARIANT_GET(variant VARIANT, path VARCHAR) -> VARIANT`; `TRY_VARIANT_GET(variant VARIANT, path VARCHAR AS type) -> type`; non-throwing variant extraction. | A failed target-type cast returns `NULL`; the public examples use the `AS type` form. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TRY_VARIANT_GET/) |
| TYPEOF | `TYPEOF(expression) -> VARCHAR`; type name. | Input expression is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TYPEOF/) |
| VARIANT_GET | `VARIANT_GET(variant VARIANT, path VARCHAR) -> VARIANT`; `VARIANT_GET(variant VARIANT, path VARCHAR AS type) -> type`; variant extraction. | The path starts with `$`; `AS type` extracts and casts, while no `AS` returns a `VARIANT`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/VARIANT_GET/) |

```sql
SELECT VARIANT_GET(PARSE_JSON('{"age": 30}'), '$.age' AS INT);

SELECT TRY_VARIANT_GET(PARSE_JSON(payload), '$.status' AS VARCHAR)
FROM events;
```
