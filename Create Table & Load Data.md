### Create table in Snowflake

```sql
# Creating table and meta data:
CREATE TABLE DatabaseName.SchemaName.TableName (
  Loan_ID STRING,
  Loan_Status STRING,
  Principal STRING,
  Terms STRING,
  Effective_Date STRING,
  Due_Date STRING,
  Age INTEGER,
  Education STRING,
  Gender STRING);
  
# Check whether the table ie empty:
SELECT * FROM DatabaseName.SchemaName.TableName;

# Loading the data from S3 bucket:
COPY INTO DatabaseName.SchemaName.TableName
FROM s3://bucketsnowflake/data.csv
file_format = (type = csv field_delimiter = ',', skip_header = 1);

# Check table:
SELECT * FROM DatabaseName.SchemaName.TableName;
```
