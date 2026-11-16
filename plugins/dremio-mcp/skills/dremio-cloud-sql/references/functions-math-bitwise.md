# Math and bitwise functions

Cloud SQL functions in the Math and Bitwise categories. Aggregate standard-deviation functions are cross-listed in Math.

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| ABS | `ABS(numeric_expression NUMERIC) -> NUMERIC`; absolute value. | Accepts binary, decimal, double, float, or integer. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ABS/) |
| ACOS | `ACOS(numeric_expression NUMERIC) -> FLOAT`; inverse cosine. | Input may be double, integer, bigint, decimal, or float. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ACOS/) |
| ASIN | `ASIN(numeric_expression NUMERIC) -> FLOAT`; inverse sine. | Input may be double, integer, or float. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ASIN/) |
| ATAN | `ATAN(inputValue FLOAT) -> FLOAT`; inverse tangent. | Input range is unbounded. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ATAN/) |
| ATAN2 | `ATAN2(y NUMERIC, x NUMERIC) -> DOUBLE`; two-coordinate inverse tangent. | Both operands are numeric coordinates. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ATAN2/) |
| BROUND | `BROUND(numeric_expression DOUBLE) -> FLOAT8`; banker's rounding. | Input is numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BROUND/) |
| CBRT | `CBRT(numeric_expression NUMERIC) -> FLOAT`; cube root. | Input can be double, float, or integer. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CBRT/) |
| CEILING | `CEILING(numeric_expression NUMERIC) -> INTEGER`; rounds up. | Input can be double, float, or integer. For a `DECIMAL(p, s)` input, the [changelog](https://docs.dremio.com/dremio-cloud/changelog/) documents a `DECIMAL(p - s + 1, 0)` result. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CEILING/) |
| COS | `COS(numeric_expression NUMERIC) -> FLOAT`; cosine. | Input is radians. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COS/) |
| COSH | `COSH(numeric_expression NUMERIC) -> FLOAT`; hyperbolic cosine. | Input is radians. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COSH/) |
| COT | `COT(numeric_expression NUMERIC) -> FLOAT`; cotangent. | Input is radians. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/COT/) |
| DEGREES | `DEGREES(numeric_expression NUMERIC) -> FLOAT`; radians to degrees. | Input may be double, integer, or float. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/DEGREES/) |
| EXP | `EXP(numeric_expression NUMERIC) -> FLOAT`; e raised to input. | Input may be double, integer, or float. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/EXP/) |
| FACTORIAL | `FACTORIAL(expression INTEGER) -> BIGINT`; factorial. | Input must be an integer from 0 through 20. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/FACTORIAL/) |
| FLOOR | `FLOOR(numeric_expression NUMERIC) -> INTEGER`; rounds down. | Input can be double, float, or integer. For a `DECIMAL(p, s)` input, the [changelog](https://docs.dremio.com/dremio-cloud/changelog/) documents a `DECIMAL(p - s + 1, 0)` result. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/FLOOR/) |
| LN | `LN(numeric_expression DOUBLE) -> FLOAT8`; natural logarithm. | Input must be greater than zero. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LN/) |
| LOG | `LOG([base_expression FLOAT], expression FLOAT) -> DOUBLE`; logarithm. | Base is optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LOG/) |
| LOG10 | `LOG10(expression DOUBLE) -> DOUBLE`; base-10 logarithm. | Input is double. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LOG10/) |
| MOD | `MOD(numeric_expression INT64, numeric_expression INT64) -> INT64`; remainder. | Both operands are `INT64`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/MOD/) |
| PI | `PI() -> DOUBLE`; pi constant. | No arguments. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/PI/) |
| PMOD | `PMOD(dividend NUMERIC, divisor NUMERIC) -> NUMERIC`; positive modulo. | Both operands are numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/PMOD/) |
| POW, POWER | `POW(numeric_expression DOUBLE, power DOUBLE) -> FLOAT8`; raises input to power. | `POWER` is the documented alias. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/POW__POWER/) |
| RADIANS | `RADIANS(x NUMBER) -> FLOAT`; degrees to radians. | Input is degrees. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/RADIANS/) |
| RANDOM | `RANDOM([seed INT32]) -> DOUBLE`; random value. | A seed yields a repeatable sequence. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/RANDOM/) |
| ROUND | `ROUND(numeric_expression DECIMAL(0,0), scale INT32) -> DECIMAL(0,0)`<br>`ROUND(numeric_expression DECIMAL(0,0)) -> DECIMAL(0,0)`<br>`ROUND(numeric_expression INT32, scale INT32) -> INT32`<br>`ROUND(numeric_expression INT32) -> INT32`<br>`ROUND(numeric_expression INT64, scale INT32) -> INT64`<br>`ROUND(numeric_expression INT64) -> INT64`<br>`ROUND(numeric_expression DOUBLE, scale INT32) -> DOUBLE`<br>`ROUND(numeric_expression DOUBLE) -> DOUBLE`<br>`ROUND(numeric_expression FLOAT, scale INT32) -> FLOAT`<br>`ROUND(numeric_expression FLOAT) -> FLOAT`. | Where present, `scale` selects the decimal place. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/ROUND/) |
| SIGN | `SIGN(numeric_expression DOUBLE) -> INT`; sign indicator. | Input is double. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SIGN/) |
| SIN | `SIN(numeric_expression INT32) -> DOUBLE`; sine. | Input is radians. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SIN/) |
| SINH | `SINH(numeric_expression INT32) -> DOUBLE`; hyperbolic sine. | Input is `INT32`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SINH/) |
| SQRT | `SQRT(numeric_expression DOUBLE) -> DOUBLE`; square root. | Input is double. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SQRT/) |
| STDDEV | `STDDEV(col_name NUMERIC) -> DOUBLE`; standard deviation. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV/) |
| STDDEV_POP | `STDDEV_POP(col_name NUMERIC) -> DOUBLE`; population standard deviation. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV_POP/) |
| STDDEV_SAMP | `STDDEV_SAMP(col_name NUMERIC) -> DOUBLE`; sample standard deviation. | Column values must be numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/STDDEV_SAMP/) |
| TAN | `TAN(numeric_expression NUMERIC) -> FLOAT`; tangent. | Input is radians. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TAN/) |
| TANH | `TANH(numeric_expression DOUBLE) -> DOUBLE`; hyperbolic tangent. | Input is double. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TANH/) |
| TRUNCATE | `TRUNCATE(numeric_expression FLOAT) -> INT`<br>`TRUNCATE(numeric_expression DOUBLE) -> INT`<br>`TRUNCATE(numeric_expression INT32) -> INT32`<br>`TRUNCATE(numeric_expression INT64) -> INT64`<br>`TRUNCATE(numeric_expression DECIMAL(0,0)) -> DECIMAL(0,0)`<br>`TRUNCATE(numeric_expression DECIMAL(0,0) [, scale_expression INT32]) -> DECIMAL(0,0)`<br>`TRUNCATE(numeric_expression INT64 [, scale_expression INT32]) -> INT64`<br>`TRUNCATE(numeric_expression FLOAT [, scale_expression INT32]) -> FLOAT`<br>`TRUNCATE(numeric_expression INT32 [, scale_expression INT32]) -> INT32`<br>`TRUNCATE(numeric_expression DOUBLE [, scale_expression INT32]) -> DOUBLE`. | Optional scale truncates after the decimal point for positive values and before it for negative values. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TRUNCATE/) |
| BITWISE_AND | `BITWISE_AND(op1 NUMERIC, op2 NUMERIC) -> NUMERIC`; bitwise AND. | Both operands are numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BITWISE_AND/) |
| BITWISE_NOT | `BITWISE_NOT(op1 NUMERIC) -> NUMERIC`; bitwise inversion. | Operand is numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BITWISE_NOT/) |
| BITWISE_OR | `BITWISE_OR(op1 NUMERIC, op2 NUMERIC) -> NUMERIC`; bitwise OR. | Both operands are numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BITWISE_OR/) |
| BITWISE_XOR | `BITWISE_XOR(op1 NUMERIC, op2 NUMERIC) -> NUMERIC`; bitwise exclusive OR. | Both operands are numeric. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BITWISE_XOR/) |
| BIT_AND | `BIT_AND(expression INT) -> INT`; aggregate bitwise AND. | Expression must be castable to integer. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BIT_AND/) |
| BIT_OR | `BIT_OR(expression INT) -> INT`; aggregate bitwise OR. | Expression must be castable to integer. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/BIT_OR/) |
| LSHIFT | `LSHIFT(expression1 INT32, expression2 INT32) -> INT32`; left shift. | Shift count is `INT32`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LSHIFT/) |
| RSHIFT | `RSHIFT(expression1 INT32, expression2 INT32) -> INT32`; right shift. | Shift count is `INT32`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/RSHIFT/) |
| XOR | `XOR(expression1 INT32, expression2 INT32) -> INT32`; exclusive OR. | Both operands are `INT32`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/XOR/) |
