# `DDL` : Data Definition Language

### `CREATE`
```sql

USE ROLE RoleName;
CREATE TABLE IF NOT EXISTS DatabaseName.SchemaName.TableName 
AS 
SELECT * FROM Database.Schema.TableName 
LIMIT 100;
```

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.TableName()
RETURNS VARCHAR
LANGUAGE SQL
EXECUTE AS CALLER
AS
$$
BEGIN
CREATE TABLE IF NOT EXISTS DatabaseName.SchemaName.TableName 
AS 
SELECT * FROM DatabaseName.SchemaName.TableName 
LIMIT 100; 
END;
$$;
```
