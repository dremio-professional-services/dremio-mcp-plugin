# Users, roles, grants, and revokes

Sources: [CREATE USER](https://docs.dremio.com/dremio-cloud/sql/commands/create-user/),
[DROP USER](https://docs.dremio.com/dremio-cloud/sql/commands/drop-user/),
[CREATE ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/create-role/),
[DROP ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/drop-role/),
[GRANT ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/grant-role/),
[REVOKE ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/revoke-role/),
[GRANT TO ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/grant-to-role/),
[GRANT TO USER](https://docs.dremio.com/dremio-cloud/sql/commands/grant-to-user/),
[REVOKE FROM ROLE](https://docs.dremio.com/dremio-cloud/sql/commands/revoke-from-role/),
and [REVOKE FROM USER](https://docs.dremio.com/dremio-cloud/sql/commands/revoke-from-user/).

## Principal lifecycle and membership

```sql
CREATE USER <username>;
DROP USER <username>;
CREATE ROLE <role_name>;
DROP ROLE <role_name>;

GRANT ROLE <role_name> TO { ROLE | USER } <role_or_user_name>;
REVOKE ROLE <role_name> FROM { ROLE | USER } <role_or_user_name>;
```

Quote a username or role name if needed by identifier rules. Removing an
externally managed user does not block a later external sign-in from creating a
new account.

## Object privileges

```sql
GRANT { <privilege> | ALL } ON <object_type> <object_name>
TO ROLE <role_name>;

REVOKE { <privilege> | ALL } ON <object_type> <object_name>
FROM ROLE <role_name>;
```

Use `TO USER` or `FROM USER` for direct user grants. The command pages also
document `ON ALL FOLDERS IN CATALOG` and `ON ALL DATASETS IN CATALOG` forms,
plus `ON ALL SPACES` and `ON ALL FOLDERS IN SPACE <space_name>`; `SPACE` is a
grantable object type.

```sql
GRANT SELECT ON ALL SPACES TO ROLE analyst;
GRANT SELECT ON ALL FOLDERS IN SPACE sales_data TO ROLE analyst;
REVOKE SELECT ON ALL FOLDERS IN SPACE sales_data FROM USER user1;
```
For `ORG` and `PROJECT`, omit the object name because it is inferred.

```sql
GRANT SELECT ON TABLE lakehouse.sales.orders TO ROLE analysts;
REVOKE SELECT ON TABLE lakehouse.sales.orders FROM ROLE analysts;
```

The eligible privileges depend on the object type. In particular, `DELETE`,
`INSERT`, `TRUNCATE`, and `UPDATE` are documented only for Iceberg tables, and
`CREATE TABLE` and `DROP` only for sources that support mutability. Confirm both
the object type and privilege before executing a change.
