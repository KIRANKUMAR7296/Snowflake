# `DDL` : Data Definition Language

### `CREATE`
```sql

USE ROLE RoleName;
CREATE TABLE IF NOT EXISTS Database.Schema.TableName 
AS 
SELECT * FROM Database.Schema.TableName 
LIMIT 100;
```

```sql
CREATE OR REPLACE PROCEDURE Database.Schema.ProcedureName()
RETURNS VARCHAR
LANGUAGE SQL
EXECUTE AS CALLER
AS
$$
BEGIN
CREATE TABLE IF NOT EXISTS Database.Schema.TableName 
AS 
SELECT * FROM Database.Schema.TableName 
LIMIT 100; 
END;
$$;
```
