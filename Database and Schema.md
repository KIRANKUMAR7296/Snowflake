# Database and Schema

`Database objects` : `Schema`, `Table` and `View`

### `Databases` and `schemas` are used to organize data stored in Snowflake.
- `Database` is a logical grouping of schemas.
- `Schema` is a logical grouping of database objects (tables, views, etc.)
- Each schema belongs to a single database.
- A database and schema comprise a `namespace` in Snowflake.
- When performing any operations on database objects in Snowflake.
- The `namespace` is inferred from the current database and schema in use.
- `Snowflake` provides a full set of `DDL` commands for creating and managing `databases` and `schemas`

```sql
-- Namespace:
`DatabaseName.SchemaName.TableName` or `DatabaseName.SchemaName.ViewName`
```
