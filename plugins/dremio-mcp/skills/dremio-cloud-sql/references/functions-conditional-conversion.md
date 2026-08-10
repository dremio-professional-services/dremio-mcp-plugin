# Boolean, conditional, conversion, and datatype functions

Cloud SQL functions in the Boolean, Conditional, Conversion, and Datatype categories.

## Boolean and conditional

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| IS [NOT] DISTINCT FROM | `expression IS [NOT] DISTINCT FROM expression -> BOOLEAN`; null-safe comparison. | The optional `NOT` reverses the comparison. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__DISTINCT_FROM/) |
| ISDATE | `ISDATE(expression) -> BOOLEAN`; date validity test. | Tests a date representation. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ISDATE/) |
| IS [NOT] FALSE | `expression IS [NOT] FALSE -> BOOLEAN`; boolean truth test. | `NOT` reverses the test. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__FALSE/) |
| IS [NOT] NULL | `expression IS [NOT] NULL -> BOOLEAN`; null test. | `NOT` tests non-null values. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__NULL/) |
| ISNUMERIC | `ISNUMERIC(expression) -> BOOLEAN`; numeric validity test. | Tests a numeric representation. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ISNUMERIC/) |
| IS [NOT] TRUE | `expression IS [NOT] TRUE -> BOOLEAN`; boolean truth test. | `NOT` reverses the test. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__TRUE/) |
| IS_MEMBER | `IS_MEMBER(expression VARCHAR) -> BOOLEAN`; Dremio-role membership test. | Tests whether the current user belongs to the named role; it can be pulled out during Reflection materialization and reapplied at query time. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_MEMBER/) |
| IS_SUBSTR | `IS_SUBSTR(expression, substring) -> BOOLEAN`; substring test. | Input and substring are compared. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_SUBSTR/) |
| BOOL_AND | `BOOL_AND(bool_expression1 BOOLEAN, bool_expression2 BOOLEAN) -> BOOLEAN`; logical AND of two expressions. | Returns `TRUE` only when both expressions are `TRUE`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BOOL_AND/) |
| BOOL_OR | `BOOL_OR(bool_expression1 BOOLEAN, bool_expression2 BOOLEAN) -> BOOLEAN`; logical OR of two expressions. | Returns `TRUE` when either expression is `TRUE`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BOOL_OR/) |
| CASE | `CASE WHEN condition THEN result [ ... ] [ELSE result] END -> result`; conditional result. | Conditions are evaluated in order. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CASE/) |
| COALESCE | `COALESCE(expression [, expressionN]) -> first non-null expression`; null fallback. | Returns the first non-null argument. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COALESCE/) |
| GREATEST | `GREATEST(expression [, expressionN]) -> expression`; greatest value. | Arguments must be comparable. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/GREATEST/) |
| LEAST | `LEAST(expression [, expressionN]) -> expression`; least value. | Arguments must be comparable. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LEAST/) |
| NULLIF | `NULLIF(expression1, expression2) -> expression1 or NULL`; equal values become null. | Compares two expressions. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/NULLIF/) |
| NVL | `NVL(expression1, expression2) -> expression`; null fallback. | Uses second expression only if first is null. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/NVL/) |

## Conversion

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| ARRAY_TO_STRING | `ARRAY_TO_STRING(list, delimiter) -> VARCHAR`; list serialization. | Delimiter is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ARRAY_TO_STRING/) |
| BINARY_STRING | `BINARY_STRING(expression VARCHAR) -> VARBINARY`; string-to-binary value. | Input is varchar. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BINARY_STRING/) |
| CAST | `CAST(expression AS data_type) -> data_type`; explicit conversion. | Target must be a supported SQL type. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CAST/) |
| CONVERT_FROM | `CONVERT_FROM(expression VARBINARY, encoding VARCHAR) -> value`; decodes binary data. | Encoding selects the input format. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CONVERT_FROM/) |
| CONVERT_REPLACEUTF8 | `CONVERT_REPLACEUTF8(expression VARBINARY, replacement VARCHAR) -> VARCHAR`; decodes invalid UTF-8 with replacement. | Replacement is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CONVERT_REPLACEUTF8/) |
| CONVERT_TIMEZONE | `CONVERT_TIMEZONE([sourceTimezone STRING], destinationTimezone STRING, timestamp DATE or TIMESTAMP or ISO-8601 STRING) -> TIMESTAMP`; timezone conversion. | The source timezone is optional and defaults to UTC. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CONVERT_TIMEZONE/) |
| CONVERT_TO | `CONVERT_TO(expression, encoding VARCHAR) -> VARBINARY`; encodes a value. | Encoding selects the output format. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CONVERT_TO/) |
| ENCODE | `ENCODE(expression STRING, charSet_type STRING) -> VARBINARY`; charset encoding. | Charset must be one of the documented accepted charsets. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ENCODE/) |
| FROM_HEX | `FROM_HEX(in STRING) -> BINARY`; hex decoding. | Input is hexadecimal text. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/FROM_HEX/) |
| FROM_UTC_TIMESTAMP | `FROM_UTC_TIMESTAMP(timestamp, timezone) -> TIMESTAMP`; converts UTC timestamp. | Timezone is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/FROM_UTC_TIMESTAMP/) |
| HASH | `HASH(expression) -> INT`; hash value. | Input expression is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/HASH/) |
| HASH64 | `HASH64(value ANY [, seed BIGINT]) -> BIGINT`; 64-bit hash value. | Value is required; seed is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/HASH64/) |
| HEX | `HEX(expression ANY PRIMITIVE) -> VARCHAR`; hex encoding. | Input must be primitive. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/HEX/) |
| STRING_BINARY | `STRING_BINARY(expression VARBINARY) -> VARCHAR`; binary-to-string value. | Input is binary. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STRING_BINARY/) |
| ST_FROMGEOHASH | `ST_FROMGEOHASH(geohash VARCHAR) -> STRUCT<latitude: DOUBLE, longitude: DOUBLE>`; geohash decoding. | Input is a geohash string. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ST_FROMGEOHASH/) |
| ST_GEOHASH | `ST_GEOHASH(latitude DOUBLE, longitude DOUBLE [, precision INTEGER]) -> VARCHAR`; geohash encoding. | Precision is 1–20. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ST_GEOHASH/) |
| TOASCII | `TOASCII(string_expression STRING, character_encoding TYPE) -> STRING`; encoding conversion. | Character encoding is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TOASCII/) |
| TO_CHAR | `TO_CHAR(expression TIME, format VARCHAR) -> VARCHAR` plus documented date/timestamp and numeric typed overloads; formatted text. | Format is required for every documented overload. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_CHAR/) |
| TO_DATE | `TO_DATE(in TIMESTAMP) -> DATE`<br>`TO_DATE(numeric_expression DOUBLE) -> DATE`<br>`TO_DATE(numeric_expression FLOAT) -> DATE`<br>`TO_DATE(numeric_expression INT32) -> DATE`<br>`TO_DATE(numeric_expression INT64) -> DATE`<br>`TO_DATE(string_expression VARCHAR, format VARCHAR) -> DATE`<br>`TO_DATE(string_expression VARCHAR, format VARCHAR, replaceErrorWithNull INT32) -> DATE`. | String forms require format; `replaceErrorWithNull` is `0` to fail or `1` to return `NULL`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_DATE/) |
| TO_HEX | `TO_HEX(in BINARY) -> STRING`; hex encoding. | Input is binary. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_HEX/) |
| TO_NUMBER | `TO_NUMBER(expression VARCHAR, format VARCHAR) -> DOUBLE`; formatted numeric conversion. | Format is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_NUMBER/) |
| TO_TIME | `TO_TIME(numeric_expression DOUBLE) -> TIME`<br>`TO_TIME(numeric_expression FLOAT) -> TIME`<br>`TO_TIME(numeric_expression INT32) -> TIME`<br>`TO_TIME(numeric_expression INT64) -> TIME`<br>`TO_TIME(string_expression VARCHAR, format VARCHAR) -> TIME`<br>`TO_TIME(string_expression VARCHAR, format VARCHAR, replaceErrorWithNull INT32) -> TIME`. | Numeric forms use Unix epoch timestamps; string forms require format; `0` fails and `1` returns `NULL`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_TIME/) |
| TO_TIMESTAMP | `TO_TIMESTAMP(numeric_expression DOUBLE) -> TIMESTAMP`<br>`TO_TIMESTAMP(numeric_expression FLOAT) -> TIMESTAMP`<br>`TO_TIMESTAMP(numeric_expression INT32) -> TIMESTAMP`<br>`TO_TIMESTAMP(numeric_expression INT64) -> TIMESTAMP`<br>`TO_TIMESTAMP(string_expression VARCHAR, format VARCHAR [, replaceErrorWithNull INT32]) -> TIMESTAMP`. | Numeric forms use Unix epoch timestamps; string form requires format; `0` fails and `1` returns `NULL`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_TIMESTAMP/) |
| TO_UTC_TIMESTAMP | `TO_UTC_TIMESTAMP(timestamp, timezone) -> TIMESTAMP`; converts local timestamp to UTC. | Timezone is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_UTC_TIMESTAMP/) |
| TO_VARIANT | `TO_VARIANT(expression) -> VARIANT`; variant conversion. | Input expression is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TO_VARIANT/) |
| TRY_CONVERT_FROM | `TRY_CONVERT_FROM(expression VARBINARY, encoding VARCHAR) -> value or NULL`; non-throwing binary decode. | Conversion failures return null. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TRY_CONVERT_FROM/) |
| UNHEX | `UNHEX(expression VARCHAR) -> VARBINARY`; hex decoding. | Non-hex input returns `NULL`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/UNHEX/) |

## Datatype

`GENERATE_UUID() -> UUID` creates a UUID; `SIZE(input MAP) -> INT` reports the
number of map entries; and `TYPEOF(expression) -> VARCHAR` reports a value type.
The `IS_*` functions below return `BOOLEAN` and test the named type or null
state.

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| GENERATE_UUID | `GENERATE_UUID() -> UUID`; creates a UUID. | No arguments. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/GENERATE_UUID/) |
| IS [NOT] DISTINCT FROM, ISDATE, IS [NOT] FALSE, IS [NOT] NULL, IS [NOT] TRUE, IS_SUBSTR | Each returns `BOOLEAN` using the Boolean-category syntax above. | These functions are cross-listed in Datatype. | [DISTINCT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__DISTINCT_FROM/), [ISDATE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ISDATE/), [FALSE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__FALSE/), [NULL](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__NULL/), [TRUE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS__NOT__TRUE/), [IS_SUBSTR](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_SUBSTR/) |
| IS_BIGINT, IS_INT, IS_VARCHAR | `IS_type(expression ANY) -> BOOLEAN`; type test. | These three type predicates accept any input. | [IS_BIGINT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_BIGINT/), [IS_INT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_INT/), [IS_VARCHAR](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_VARCHAR/) |
| IS_BOOLEAN, IS_DATE, IS_DECIMAL, IS_DOUBLE, IS_FLOAT, IS_LIST, IS_STRUCT, IS_TIMESTAMP, IS_TIME, IS_UUID, IS_VARBINARY | `IS_type(value VARIANT) -> BOOLEAN`; type test. | These predicates require `VARIANT` input. | [IS_BOOLEAN](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_BOOLEAN/), [IS_DATE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_DATE/), [IS_DECIMAL](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_DECIMAL/), [IS_DOUBLE](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_DOUBLE/), [IS_FLOAT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_FLOAT/), [IS_LIST](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_LIST/), [IS_STRUCT](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_STRUCT/), [IS_TIMESTAMP](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_TIMESTAMP/), [IS_TIME](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_TIME/), [IS_UUID](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_UUID/), [IS_VARBINARY](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_VARBINARY/) |
| IS_VARIANT_NULL | `IS_VARIANT_NULL(variant VARIANT) -> BOOLEAN`; tests a `VARIANT<NULL>` value. | It is distinct from SQL `NULL`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/IS_VARIANT_NULL/) |
| SIZE | `SIZE(input MAP) -> INT`; map entry count. | Input must be a map expression. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SIZE/) |
| TYPEOF | `TYPEOF(expression) -> VARCHAR`; value type name. | Input expression is required. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TYPEOF/) |
