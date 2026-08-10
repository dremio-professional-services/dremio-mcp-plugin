# Boolean, Conditional, Conversion, and Datatype functions

Scope: Dremio Enterprise current [26.x]. Follow the individual public page for format strings, encodings, and error behavior.

| Function | Documented syntax | Result | Constraint |
| --- | --- | --- | --- |
| [IS [NOT] DISTINCT FROM](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS__NOT__DISTINCT_FROM/) | `a IS [NOT] DISTINCT FROM b → boolean` | Null-safe equality predicate | Operator, not call. |
| [IS [NOT] FALSE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS__NOT__FALSE/) | `boolean IS [NOT] FALSE → boolean` | False predicate | Boolean input only. |
| [IS [NOT] NULL](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS__NOT__NULL/) | `any IS [NOT] NULL → boolean` | Null predicate | Accepts any input. |
| [IS [NOT] TRUE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS__NOT__TRUE/) | `int32\|int64\|boolean IS [NOT] TRUE → boolean` | True predicate | Limited to documented input types. |
| [ISDATE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ISDATE/) | `ISDATE(expression varchar) → boolean` | Whether input parses as date | Varchar input. |
| [ISNUMERIC](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ISNUMERIC/) | `ISNUMERIC(expression varchar) → boolean` | Whether input parses as number | Varchar input. |
| [IS_MEMBER](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS_MEMBER/) | `IS_MEMBER(expression varchar) → boolean` | Whether current user is member of role | In reflections it may be evaluated at materialization and query time. |
| [IS_SUBSTR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS_SUBSTR/) | `IS_SUBSTR(string varchar, substring varchar) → boolean` | Substring predicate | Varchar arguments. |
| [BOOL_AND](https://docs.dremio.com/current/reference/sql/sql-functions/functions/BOOL_AND/) | `BOOL_AND(boolean, boolean) → boolean` | Boolean conjunction | Boolean input pair. |
| [BOOL_OR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/BOOL_OR/) | `BOOL_OR(boolean, boolean) → boolean` | Boolean disjunction | Boolean input pair. |
| [CASE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CASE/) | `CASE expression WHEN condition THEN result [n] ELSE result END → same input type`; `CASE WHEN condition THEN result [n] ELSE result END → same input type` | First matching result | All result expressions resolve to one type. |
| [COALESCE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/COALESCE/) | `COALESCE(expression1, expression2 [, expressionN]) → input type` | First non-null value | Compatible argument types. |
| [NVL](https://docs.dremio.com/current/reference/sql/sql-functions/functions/NVL/) | `NVL(expression1, expression2) → input type` | First non-null value | Exactly two compatible arguments. |
| [GREATEST](https://docs.dremio.com/current/reference/sql/sql-functions/functions/GREATEST/) | `GREATEST(expression1, expression2 [, expressionN]) → input type` | Greatest value | Compatible arguments. |
| [LEAST](https://docs.dremio.com/current/reference/sql/sql-functions/functions/LEAST/) | `LEAST(expression1, expression2 [, expressionN]) → input type` | Least value | Compatible arguments. |
| [NULLIF](https://docs.dremio.com/current/reference/sql/sql-functions/functions/NULLIF/) | `NULLIF(value1 any, value2 any) → same as value1` | Null if equal; otherwise first value | Comparable arguments. |
| [ARRAY_TO_STRING](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ARRAY_TO_STRING/) | `ARRAY_TO_STRING(arr list, delimiter varchar) → varchar` | Delimited string | Array input. |
| [BINARY_STRING](https://docs.dremio.com/current/reference/sql/sql-functions/functions/BINARY_STRING/) | `BINARY_STRING(expression varchar) → binary` | Binary conversion | Varchar input. |
| [STRING_BINARY](https://docs.dremio.com/current/reference/sql/sql-functions/functions/STRING_BINARY/) | `STRING_BINARY(bytes) → string` | String conversion | Bytes input. |
| [CAST](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CAST/) | `CAST(expression any AS data_type) → specified data_type` | Converted value | Invalid casts fail. |
| [CONVERT_FROM](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CONVERT_FROM/) | `CONVERT_FROM(binary_value, data_type) → varies` | Decoded value | First argument is binary. |
| [CONVERT_TO](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CONVERT_TO/) | `CONVERT_TO(value, data_type) → varbinary` | Encoded value | Data-type name is required. |
| [TRY_CONVERT_FROM](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TRY_CONVERT_FROM/) | `TRY_CONVERT_FROM(value_to_convert string AS data_type) → any` | Safely coerced value | Uses `AS`; target `data_type` is `ROW` or `ARRAY` only. |
| [CONVERT_REPLACEUTF8](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CONVERT_REPLACEUTF8/) | `CONVERT_REPLACEUTF8(binary_value, replacement varchar) → varchar` | UTF-8 string with replacement | Binary input. |
| [CONVERT_TIMEZONE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CONVERT_TIMEZONE/) | `CONVERT_TIMEZONE([sourceTimezone string], destinationTimezone string, timestamp date\|timestamp\|ISO-8601 string) → timestamp` | Time-zone-adjusted timestamp | Time-zone identifiers valid. |
| [ENCODE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ENCODE/) | `ENCODE(expression varchar, charSet_type varchar) → varbinary` | Encoded value | Charset type is required. |
| [FROM_HEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/FROM_HEX/) | `FROM_HEX(expression varchar) → varbinary` | Decoded hex bytes | Varchar input. |
| [HEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/HEX/) | `HEX(expression varbinary) → varchar` | Hex string | Binary input. |
| [TO_HEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TO_HEX/) | `TO_HEX(binary) → string` | Hex string | Binary input. |
| [UNHEX](https://docs.dremio.com/current/reference/sql/sql-functions/functions/UNHEX/) | `UNHEX(expression varchar) → varbinary` | Decoded hex bytes | Varchar input. |
| [HASH](https://docs.dremio.com/current/reference/sql/sql-functions/functions/HASH/) | `HASH(expression any) → int32` | 32-bit hash | Not cryptographic. |
| [HASH64](https://docs.dremio.com/current/reference/sql/sql-functions/functions/HASH64/) | `HASH64(value any [, seed bigint]) → bigint` | 64-bit hash | `seed` is optional; not cryptographic. |
| [ST_FROMGEOHASH](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ST_FROMGEOHASH/) | `ST_FROMGEOHASH(geohash varchar) → struct<latitude: double, longitude: double>` | Coordinates from geohash | Varchar geohash input. |
| [ST_GEOHASH](https://docs.dremio.com/current/reference/sql/sql-functions/functions/ST_GEOHASH/) | `ST_GEOHASH(latitude double, longitude double [, precision integer]) → varchar` | Geohash | Latitude/longitude order is required. |
| [TOASCII](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TOASCII/) | `TOASCII(string_expression string, character_encoding type) → string` | ASCII representation | Encoding required. |
| [TO_CHAR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TO_CHAR/) | `TO_CHAR(time\|date\|int32\|int64\|float\|double\|timestamp, format varchar) → varchar` | Formatted temporal/numeric value | Format is required. |
| [TO_DATE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TO_DATE/) | `TO_DATE(timestamp\|int32\|int64\|float\|double) → date`; `TO_DATE(varchar, format [, replaceErrorWithNull int32]) → date` | Parsed date | Third string argument is `INT32` null flag. |
| [TO_TIME](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TO_TIME/) | `TO_TIME(int32\|int64\|float\|double) → time`; `TO_TIME(varchar, format [, replaceErrorWithNull int32]) → time` | Parsed time | Third string argument is `INT32` null flag. |
| [TO_TIMESTAMP](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TO_TIMESTAMP/) | `TO_TIMESTAMP(int32\|int64\|float\|double) → timestamp`; `TO_TIMESTAMP(varchar, format [, replaceErrorWithNull int32]) → timestamp` | Parsed timestamp | Third string argument is `INT32` null flag. |
| [TO_NUMBER](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TO_NUMBER/) | `TO_NUMBER(expression varchar, format varchar) → double` | Numeric value | Input must match format. |
| [IS_BIGINT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS_BIGINT/) | `IS_BIGINT(value any) → boolean` | BIGINT type predicate | Tests only BIGINT. |
| [IS_INT](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS_INT/) | `IS_INT(value any) → boolean` | INT type predicate | Tests only INT. |
| [IS_VARCHAR](https://docs.dremio.com/current/reference/sql/sql-functions/functions/IS_VARCHAR/) | `IS_VARCHAR(value any) → boolean` | VARCHAR type predicate | Tests only VARCHAR. |
| [SIZE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SIZE/) | `SIZE(input map) → int` | Map size | Map input. |
| [TYPEOF](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TYPEOF/) | `TYPEOF(input any) → varchar` | Type name | Result is type description. |
