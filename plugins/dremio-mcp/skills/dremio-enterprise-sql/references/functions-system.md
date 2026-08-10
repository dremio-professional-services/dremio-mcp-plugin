# System functions

Scope: Dremio Enterprise current [26.x]. Current-value functions reflect the query/session context documented on their individual pages.

| Function | Documented syntax | Result | Constraint |
| --- | --- | --- | --- |
| [CURRENT_DATE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CURRENT_DATE/) | `CURRENT_DATE\|CURRENT_DATE() → date` | Current local date | Current page permits bare and parenthesized forms. |
| [CURRENT_DATE_UTC](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CURRENT_DATE_UTC/) | `CURRENT_DATE_UTC\|CURRENT_DATE_UTC() → date` | Current UTC date | Current page permits bare and parenthesized forms. |
| [CURRENT_SCHEMA](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CURRENT_SCHEMA/) | `CURRENT_SCHEMA → varchar` | Current schema name | Bare form; depends on query context. |
| [CURRENT_TIME](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CURRENT_TIME/) | `CURRENT_TIME\|CURRENT_TIME() → time` | Current time | Current page permits bare and parenthesized forms. |
| [CURRENT_TIMESTAMP](https://docs.dremio.com/current/reference/sql/sql-functions/functions/CURRENT_TIMESTAMP/) | `CURRENT_TIMESTAMP\|CURRENT_TIMESTAMP() → timestamp` | Current timestamp | Current page permits bare and parenthesized forms. |
| [LAST_QUERY_ID](https://docs.dremio.com/current/reference/sql/sql-functions/functions/LAST_QUERY_ID/) | `LAST_QUERY_ID\|LAST_QUERY_ID() → varchar` | Identifier of last query | Session/query history context required; current page permits both forms. |
| [LOCALTIME](https://docs.dremio.com/current/reference/sql/sql-functions/functions/LOCALTIME/) | `LOCALTIME() → time` | Local current time | Parentheses required. |
| [LOCALTIMESTAMP](https://docs.dremio.com/current/reference/sql/sql-functions/functions/LOCALTIMESTAMP/) | `LOCALTIMESTAMP() → timestamp` | Local current timestamp | Parentheses required. |
| [NOW](https://docs.dremio.com/current/reference/sql/sql-functions/functions/NOW/) | `NOW() → timestamp` | Current timestamp | Evaluation timing follows the public page. |
| [TRANSACTION_TIMESTAMP](https://docs.dremio.com/current/reference/sql/sql-functions/functions/TRANSACTION_TIMESTAMP/) | `TRANSACTION_TIMESTAMP() → timestamp` | Transaction timestamp | Parentheses required. |
| [QUERY_USER](https://docs.dremio.com/current/reference/sql/sql-functions/functions/QUERY_USER/) | `QUERY_USER() → varchar` | Query user identity | Parentheses required. |
| [SESSION_USER](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SESSION_USER/) | `SESSION_USER → varchar` | Session user identity | Bare keyword form. |
| [SYSTEM_USER](https://docs.dremio.com/current/reference/sql/sql-functions/functions/SYSTEM_USER/) | `SYSTEM_USER → varchar` | System user identity | Bare keyword form. |
| [USER](https://docs.dremio.com/current/reference/sql/sql-functions/functions/USER/) | `USER\|USER() → varchar` | User identity | Current page permits bare and parenthesized forms. |
| [UNIX_TIMESTAMP](https://docs.dremio.com/current/reference/sql/sql-functions/functions/UNIX_TIMESTAMP/) | `UNIX_TIMESTAMP() → int64`; `UNIX_TIMESTAMP(varchar [, format varchar]) → int64` | Epoch seconds | Unit is seconds. |
