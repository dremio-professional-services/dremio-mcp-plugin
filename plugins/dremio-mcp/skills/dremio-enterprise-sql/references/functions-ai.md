# AI functions

Scope: Dremio Enterprise current [26.x]. The current Enterprise index exposes these AI entries. Model/file binding, credentials, and availability follow each linked page.

| Function | Documented syntax | Result | Constraint |
| --- | --- | --- | --- |
| [AI_CLASSIFY](https://docs.dremio.com/current/reference/sql/sql-functions/functions/AI_CLASSIFY/) | `AI_CLASSIFY([model_name varchar,] prompt varchar \| (prompt varchar, file_reference), categories array<varchar\|int\|float\|boolean>) → varchar\|int\|float\|boolean` | AI classification | Categories have a single typed array element type; file reference is a separate tuple form. |
| [AI_COMPLETE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/AI_COMPLETE/) | `AI_COMPLETE([model_name varchar,] prompt varchar) → varchar` | AI completion text | Optional model name precedes prompt. |
| [AI_GENERATE](https://docs.dremio.com/current/reference/sql/sql-functions/functions/AI_GENERATE/) | `AI_GENERATE([model_name varchar,] prompt varchar \| (prompt varchar, file_reference) [WITH SCHEMA data_type]) → any\|row` | Generated AI result | `WITH SCHEMA` belongs only to the documented file/prompt form. |
| [LIST_FILES](https://docs.dremio.com/current/reference/sql/sql-functions/functions/LIST_FILES/) | `LIST_FILES(source_path varchar) → table`; use `TABLE(LIST_FILES('@source/path'))` | File rows beneath a source path | Table-function binding, source permissions, and supported path context required. |
