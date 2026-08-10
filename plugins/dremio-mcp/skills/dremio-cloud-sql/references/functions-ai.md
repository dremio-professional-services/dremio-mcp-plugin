# AI functions

Cloud SQL functions in the AI category. Model names reference configured model providers; these functions do not configure providers or grant access.

| Function | Documented syntax and result | Load-bearing constraint | Source |
| --- | --- | --- | --- |
| AI_CLASSIFY | `AI_CLASSIFY([model_name VARCHAR,] prompt VARCHAR or (prompt VARCHAR, file_reference), categories ARRAY<VARCHAR \| INT \| FLOAT \| BOOLEAN>) -> VARCHAR \| INT \| FLOAT \| BOOLEAN`; classifies content into a supplied category list. | Result type matches the category-array element type; omitted model uses the organization default. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/AI_CLASSIFY/) |
| AI_COMPLETE | `AI_COMPLETE([model_name VARCHAR,] prompt VARCHAR) -> VARCHAR`; produces text completion or summarization. | `model_name` is `modelProvider.modelName`; omitted model uses the organization default. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/AI_COMPLETE/) |
| AI_GENERATE | `AI_GENERATE([model_name VARCHAR,] prompt VARCHAR or (prompt VARCHAR, file_reference) [WITH SCHEMA data_type]) -> ANY or ROW`; generates structured or unstructured output. | `WITH SCHEMA` accepts JSON-valid SQL types and flat lists/rows; file input comes from `LIST_FILES`. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/AI_GENERATE/) |
| LIST_FILES | `LIST_FILES(source_path VARCHAR) -> TABLE`; returns source-directory file metadata for AI or data workflows. | Source paths use `@source_name/path/to/directory` and follow the `COPY INTO` security model. | [docs](https://docs.dremio.com/dremio-cloud/sql/sql-functions/functions/LIST_FILES/) |

```sql
SELECT AI_GENERATE(
  'provider.model',
  ('Extract fields', file)
  WITH SCHEMA ROW(title VARCHAR, published_year INT)
)
FROM TABLE(LIST_FILES('@source/documents'));
```

The optional schema makes the requested result shape explicit; provider access and model availability remain organization configuration concerns.
