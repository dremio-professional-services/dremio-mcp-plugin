# Enterprise RBAC and UDF-backed data policies

Current sources: [RBAC](https://docs.dremio.com/current/reference/sql/commands/rbac),
[roles](https://docs.dremio.com/current/reference/sql/commands/roles),
[users](https://docs.dremio.com/current/reference/sql/commands/users), and
[row-access and column-masking policies](https://docs.dremio.com/current/reference/sql/commands/row-column-policies).

## Object privileges and roles

```sql
GRANT { <objectPrivilege> [, <objectPrivilege> ]* | ALL }
  ON <object> TO <grantee>;
REVOKE { <objectPrivilege> [, <objectPrivilege> ]* | ALL }
  ON <object> FROM <grantee>;

CREATE ROLE <role_name>;
DROP ROLE <role_name>;
GRANT ROLE <role_name> TO USER <username>;
REVOKE ROLE <role_name> FROM USER <username>;
GRANT ROLE <sub_role> TO ROLE <parent_role>;
REVOKE ROLE <sub_role> FROM ROLE <parent_role>;
GRANT ROLE ADMIN TO ROLE <groupName>;
```

`<object>` is one of `<object_type> <object_name>`, `ALL DATASETS IN
{ SPACE | SOURCE | FOLDER | SCHEMA } <object_name>`, or `{ <project_name> |
SYSTEM }`. `<grantee>` is `USER <username>`, `ROLE <role_name>`, or `PROJECT
<project_name>`. Use only the current page's privilege list for the selected
object type; `OWNERSHIP` is invalid for `ALL DATASETS`. Revoke at the scope
where the privilege was granted: a higher-level grant continues to apply.

## User lifecycle

```sql
CREATE USER <username>;
ALTER USER <username> SET PASSWORD '<password>';
ALTER USER <username> UNSET PASSWORD;
DROP USER <username>;
```

`ALTER USER` password operations apply only to local users. `UNSET PASSWORD`
changes a local user to external only when the configured external service
recognizes that username. Dropping an external user does not prevent a later
external login from creating it again.

## Column masking and row access

```sql
ALTER { TABLE | VIEW } [ IF EXISTS ] <table_or_view_name>
  MODIFY COLUMN <column_name>
  SET MASKING POLICY <function_name>
    ( <column_name> [, <column_name> ]* );

ALTER { TABLE | VIEW } [ IF EXISTS ] <table_or_view_name>
  MODIFY COLUMN <column_name>
  UNSET MASKING POLICY <function_name>;

ALTER { TABLE | VIEW } [ IF EXISTS ] <table_or_view_name>
  ADD ROW ACCESS POLICY <function_name>
    ( <column_name> [, <column_name> ]* );

ALTER { TABLE | VIEW } [ IF EXISTS ] <table_or_view_name>
  DROP ROW ACCESS POLICY <function_name>
    ( <column_name> [, <column_name> ]* );
```

Policies are not standalone policy objects: the function name identifies a UDF.
A masking UDF must accept and return the masked column's data type. A missing
UDF can make the affected table or view unreachable until the policy is removed
or the UDF exists. A row-access policy can also be attached while creating a
table or view with a `ROW ACCESS POLICY` clause; use the current
policy page's complete CREATE TABLE/VIEW production for that form.
