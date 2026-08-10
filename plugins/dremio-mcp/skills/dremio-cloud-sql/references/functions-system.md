# System functions

Cloud SQL functions in the System category. Functions marked as unavailable in reflections retain that documented boundary.

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| CURRENT_DATE | `CURRENT_DATE() -> DATE`; returns the system date. | Parentheses are optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CURRENT_DATE/) |
| CURRENT_DATE_UTC | `CURRENT_DATE_UTC() -> DATE`; returns the UTC system date. | Parentheses are optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CURRENT_DATE_UTC/) |
| CURRENT_SCHEMA | `CURRENT_SCHEMA -> VARCHAR`; returns the session schema path. | Use the bare keyword, without parentheses; it cannot be used in a Reflection. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CURRENT_SCHEMA/) |
| CURRENT_TIME | `CURRENT_TIME() -> TIME`; returns the system time. | Parentheses are optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CURRENT_TIME/) |
| CURRENT_TIMESTAMP | `CURRENT_TIMESTAMP([precision INT32]) -> TIMESTAMP`; returns the current system timestamp. | `precision` controls rounding precision; parentheses are optional. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/CURRENT_TIMESTAMP/) |
| LAST_QUERY_ID | `LAST_QUERY_ID() -> VARCHAR`; returns the current session's latest query ID. | Cannot be used in a Reflection; prepared statements update it only after execution. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LAST_QUERY_ID/) |
| LOCALTIME | `LOCALTIME() -> TIME`; returns the system's current local time. | Use the no-argument form. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LOCALTIME/) |
| LOCALTIMESTAMP | `LOCALTIMESTAMP([precision INT32]) -> TIMESTAMP`; returns the current local timestamp. | Optional precision sets rounding digits. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LOCALTIMESTAMP/) |
| NOW | `NOW() -> TIMESTAMP`; returns the current UTC timestamp. | Uses UTC. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/NOW/) |
| QUERY_USER | `QUERY_USER() -> VARCHAR`; returns the logged-in user name. | Cannot be used in a Reflection. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/QUERY_USER/) |
| SESSION_USER | `SESSION_USER -> VARCHAR`; returns the user that created the session. | Cannot be used in a Reflection; it is identical to `SYSTEM_USER` and `USER`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SESSION_USER/) |
| SYSTEM_USER | `SYSTEM_USER -> VARCHAR`; returns the current user name. | Cannot be used in a Reflection; it is identical to `SESSION_USER` and `USER`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/SYSTEM_USER/) |
| TRANSACTION_TIMESTAMP | `TRANSACTION_TIMESTAMP() -> TIMESTAMP`; returns the current transaction's UTC timestamp. | Cannot be used in a Reflection. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/TRANSACTION_TIMESTAMP/) |
| UNIX_TIMESTAMP | `UNIX_TIMESTAMP() -> INT64`; `UNIX_TIMESTAMP(date_timestamp_expression VARCHAR [, format VARCHAR]) -> INT64`; returns Unix epoch time. | The unformatted varchar form expects `YYYY-MM-DD HH24:MI:SS`; a format can be supplied. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/UNIX_TIMESTAMP/) |
| USER | `USER() -> VARCHAR`; returns the logged-in user. | Cannot be used in a Reflection; parentheses are optional and it is identical to `SESSION_USER` and `SYSTEM_USER`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/USER/) |
