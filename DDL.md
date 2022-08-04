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

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.TableName()
RETURNS VARCHAR NOT NULL
LANGUAGE JAVASCRIPT
AS
$$
var sql_command = "SELECT * FROM DatabaseName.SchemaName.TableName LIMIT 100";

var statement = snowflake.createStatement({sqlText: sql_command});

var result = statement.execute();

-- Loop through the results, processing one row at a time...
var summation = 0

while (result.next())
  {
    summation = summation + result.getColumnValue(1); 
  }
 
return summation; 
$$;
```  
