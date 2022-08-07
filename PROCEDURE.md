# `PROCEDURE`

```sql
CREATE OR REPLACE PROCEDURE DatabaseName.SchemaName.ProcedureName(DateofBirth DATE)
RETURNS VARCHAR
LANGUAGE SQL
AS
DECLARE
Age NUMBER;
BEGIN
Age := DATEDIFF(YEAR, DateofBirth, CURRENT_DATE());
RETURN 'Your Age is :' || Age::VARCHAR; -- Casting data type of Age i.e NUMBER to VARCHAR.
END;

CALL DatabaseName.SchemaName.ProcedureName('1996-02-07')
``` 
