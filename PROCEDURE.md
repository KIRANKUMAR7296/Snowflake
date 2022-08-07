# `PROCEDURE`

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.ProcedureName(DateofBirth DATE)
RETURNS VARCHAR
LANGUAGE SQL
AS
DECLARE Age NUMBER;
BEGIN
Age = DATEDIFF(YEAR, DateofBirth, CURRENT_DATE());
RETURN 'Your Age is :' || Age::VARCHAR; -- Casting data type of Age i.e NUMBER to VARCHAR.
END;

CALL DatabaseName.SchemaName.ProcedureName('1996-02-07')
``` 


```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.ProcedureName(EmployeeID NUMBER)
RETURNS VARCHAR
LANGUAGE SQL
AS
DECLARE EmployeeName VARCHAR;
BEGIN
SELECT FirstName || ' ' || LastName INTO: EmployeeName 
FROM Employee
WHERE EmployeeStaffCode = EmployeeID;
RETURN 'Employee Name is :' || EmployeeName;
END;

CALL DatabaseName.SchemaName.ProcedureName(7296)
```

### `RETURN TABLE`

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.ProcedureName(EmployeeID NUMBER)
RETURNS TABLE(
EmployeeCode NUMBER(38,0),
FirstName VARCHAR(16777216),
LastName VARCHAR(16777216),
Designation VARCHAR(16777216),
Manager VARCHAR(16777216),
HiredDate VARCHAR(16777216),
Salary NUMBER(16777216),
DepartmentID NUMBER(16777216),
)
LANGUAGE SQL
AS
DECLARE Query VARCHAR = 'SELECT * FROM Employee where Employee code =' || EmployeeID
EmployeeRecord RESULTSET; 
BEGIN
EmployeeRecord = (EXECUTE IMMEDIATE: Query);
RETURN TABLE(EmployeeRecord);
END;

CALL DatabaseName.SchemaName.ProcedureName(7296)
```
