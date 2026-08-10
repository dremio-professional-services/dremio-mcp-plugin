# Semi-structured data functions

Scope: Dremio Enterprise current [26.x]. The current Enterprise index has no separate UUID Type or Variant Type category; neither is imported here.

| Function | Documented syntax | Result | Constraint |
| --- | --- | --- | --- |
| [ARRAYS_OVERLAP](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAYS_OVERLAP/) | `ARRAYS_OVERLAP(arr1 list, arr2 list) → boolean` | Whether arrays share an element | Comparable element types. |
| [ARRAY_AGG](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_AGG/) | `ARRAY_AGG([DISTINCT] expression) → array` | Array aggregate | Aggregate context. |
| [ARRAY_APPEND](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_APPEND/) | `ARRAY_APPEND(array list, element any) → list` | Array with appended element | Element must be compatible with array. |
| [ARRAY_PREPEND](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_PREPEND/) | `ARRAY_PREPEND(element any, array list) → list` | Array with prepended element | Argument order differs from `ARRAY_APPEND`. |
| [ARRAY_AVG](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_AVG/), [ARRAY_MAX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_MAX/), [ARRAY_MIN](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_MIN/), [ARRAY_SUM](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_SUM/) | `ARRAY_AVG\|ARRAY_MAX\|ARRAY_MIN\|ARRAY_SUM(list_column list) → numeric` | Numeric list aggregate | List elements must be numeric. |
| [ARRAY_CAT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_CAT/) | `ARRAY_CAT(arr1 list, arr2 list) → list` | Concatenated array | Compatible element types. |
| [ARRAY_COMPACT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_COMPACT/) | `ARRAY_COMPACT(arr list) → list` | Array without nulls | List input. |
| [ARRAY_DISTINCT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_DISTINCT/) | `ARRAY_DISTINCT(input list) → list` | Distinct array | List input. |
| [ARRAY_CONTAINS](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_CONTAINS/) | `ARRAY_CONTAINS(list list, value any) → boolean` | Containment predicate | Value must be comparable to list elements. |
| [ARRAY_POSITION](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_POSITION/) | `ARRAY_POSITION(element any, arr list) → numeric` | Element position | Element is first argument. |
| [ARRAY_FREQUENCY](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_FREQUENCY/) | `ARRAY_FREQUENCY(array list) → map` | Element frequency map | Array input. |
| [ARRAY_GENERATE_RANGE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_GENERATE_RANGE/) | `ARRAY_GENERATE_RANGE(start int32, stop int32) → list`; `ARRAY_GENERATE_RANGE(start int32, stop int32, step int32) → list` | Integer range array | `step` is optional, defaults to `1`, and cannot be `0`. |
| [ARRAY_INSERT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_INSERT/) | `ARRAY_INSERT(arr list, position int, new_element any) → list` | Array with inserted element | Position is second. |
| [ARRAY_REMOVE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_REMOVE/) | `ARRAY_REMOVE(list_column list, value any) → list` | Array with value removed | List input. |
| [ARRAY_REMOVE_AT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_REMOVE_AT/) | `ARRAY_REMOVE_AT(arr list, position int32) → list` | Array with position removed | Position is `INT32`. |
| [ARRAY_SLICE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_SLICE/) | `ARRAY_SLICE(arr list, from int, to int) → list` | Array slice | Both bounds required. |
| [ARRAY_SIZE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_SIZE/) | `ARRAY_SIZE(arr list) → numeric` | Element count | List input. |
| [CARDINALITY](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CARDINALITY/) | `CARDINALITY(list_or_map list\|map) → bigint` | List/map count | Accepts list or map. |
| [ARRAY_TO_STRING](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_TO_STRING/) | `ARRAY_TO_STRING(arr list, delimiter varchar) → varchar` | Delimited string | Array input. |
| [FLATTEN](https://docs.dremio.com/current/reference/sql/sql-functions/functions/FLATTEN/) | `FLATTEN(expression list) → list` | Expanded array elements | Use in documented query context. |
| [MAP_KEYS](https://docs.dremio.com/current/reference/sql/sql-functions/functions/MAP_KEYS/) | `MAP_KEYS(input map) → array of strings` | Map keys | Map input. |
| [MAP_VALUES](https://docs.dremio.com/current/reference/sql/sql-functions/functions/MAP_VALUES/) | `MAP_VALUES(input map) → array` | Map values | Map input. |
| [SET_UNION](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SET_UNION/) | `SET_UNION(array1 list, array2 list) → list` | Unioned array | Element types compatible. |
| [SUBLIST](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SUBLIST/) | `SUBLIST(arr list, offset int, length int) → list` | List subset | Offset and length required. |
