# `PROCEDURE`

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.CalculateAge(DateofBirth DATE)
RETURNS VARCHAR
LANGUAGE SQL
AS
DECLARE 
Age NUMBER;
BEGIN
Age = DATEDIFF(YEAR, DateofBirth, CURRENT_DATE());
RETURN 'Your Age is :' || Age::VARCHAR; -- Casting data type of Age i.e NUMBER to VARCHAR.
END;

CALL DatabaseName.SchemaName.CalculateAge('1996-02-07')
``` 


```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.FindEmployeeName(EmployeeID NUMBER)
RETURNS VARCHAR
LANGUAGE SQL
AS
DECLARE 
EmployeeName VARCHAR;
BEGIN
SELECT FirstName || ' ' || LastName INTO: EmployeeName 
FROM Employee
WHERE EmployeeStaffCode = EmployeeID;
RETURN 'Employee Name is :' || EmployeeName;
END;

CALL DatabaseName.SchemaName.FindEmployeeName(7296)
```

### `RETURN TABLE Record`

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.FindEmployeeRecord(EmployeeID NUMBER)
RETURNS TABLE(
EmployeeCode NUMBER(38,0),
FirstName VARCHAR(16777216),
LastName VARCHAR(16777216),
Designation VARCHAR(16777216),
Manager VARCHAR(16777216),
HiredDate VARCHAR(16777216),
Salary NUMBER(7,2),
DepartmentID NUMBER(7,2)
)
LANGUAGE SQL
AS
DECLARE 
Query VARCHAR := 'SELECT * FROM Employee where Employee code =' || EmployeeID
EmployeeRecord RESULTSET; 
BEGIN
EmployeeRecord := (EXECUTE IMMEDIATE: Query);
RETURN TABLE(EmployeeRecord);
END;

CALL DatabaseName.SchemaName.FindEmployeeRecord(7296)
```

### `RETURN` entire `TABLE`

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.FindEmployeeDetails()
RETURNS TABLE(
EmployeeCode NUMBER(38,0),
FirstName VARCHAR(16777216),
LastName VARCHAR(16777216),
Designation VARCHAR(16777216),
Manager VARCHAR(16777216),
HiredDate VARCHAR(16777216),
Salary NUMBER(7,2),
DepartmentID NUMBER(7,2)
)
LANGUAGE SQL
AS
DECLARE 
Query RESULTSET := (SELECT * FROM Employee);
BEGIN
RETURN TABLE(Query);
END;

CALL DatabaseName.SchemaName.FindEmployeeDetails()
```

### `CREATE` a copy of `TABLE`

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.CreateTableCopy(SourceTable VARCHAR, TargetTable VARCHAR, WhereClause VARCHAR)
RETURNS VARCHAR
LANGUAGE SQL
AS 
DECLARE

-- Create a copy of existing table:
CreateCommand VARCHAR := 'CREATE OR REPLACE TABLE ' || :TargetTable || ' LIKE ' || :SourceTable;
-- Insert values from the existing table:
InsertCommand VARCHAR := 'INSERT INTO ' || :TargetTable || ' SELECT * FROM ' || :SourceTable || ' WHERE ' || :WhereClause;

BEGIN
EXECUTE IMMEDIATE : CreateCommand;
EXECUTE IMMEDIATE : InsertCommand;

RETURN sqlrowcount::VARCHAR;
EXCEPTION
WHEN other THEN
RETURN sqlerrm; -- SQL Error Message
END;

CALL CreateTableCopy('Demand', 'AMRDemand', 'Region="AMR"')
```

### `CREATE` a copy of `TABLE` + `COUNT` Rows and Capture Error Message

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.CreateTableCopy(SourceTable VARCHAR, TargetTable VARCHAR, WhereClause VARCHAR)
RETURNS TABLE(Records NUMBER)
LANGUAGE SQL
AS 
DECLARE

-- Create a copy of existing table:
CreateCommand VARCHAR := 'CREATE OR REPLACE TABLE ' || :TargetTable || ' LIKE ' || :SourceTable;
-- Insert values from the existing table:
InsertCommand VARCHAR := 'INSERT INTO ' || :TargetTable || ' SELECT * FROM ' || :SourceTable || ' WHERE ' || :WhereClause;
-- Count the total rows in new table:
RowCount RESULTSET;
ReadCount VARCHAR := 'SELECT COUNT(*) FROM ' || :TargetTable;
-- Error Message:
ErrorMessage RESULTSET;

BEGIN
EXECUTE IMMEDIATE : CreateCommand;
EXECUTE IMMEDIATE : InsertCommand;
RowCount := (EXECUTE IMMEDIATE : ReadCount);
RETURN TABLE(RowCount);

EXCEPTION
WHEN other THEN NULL;
END;

CALL CreateTableCopy('Demand', 'AMRDemand', 'Region="AMR"')
```
