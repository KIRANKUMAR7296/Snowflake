# Stages

- Stages are just a database object that contains the location where we can load data from.
- Database object can have certain properties such as the location, connection, credentials and access settings.

### External Stage

- External Cloud Provider
- `AWS S3` Bucket
- Google Cloud Platform
- Microsoft Azure `Blob Storage`
- CREATE STAGE(URL, access_settings)
- Most frequently used.

### Internal Stage

- Local inpremise server storage maintained by snowflake. 

```sql
-- Database to manage stage objects, fileformats, etc.
CREATE OR REPLACE DATABASE MANAGE_DB;

CREATE OR REPLACE SCHEMA External_Stages;

-- Creating external stage:
CREATE OR REPLACE STAGE MANAGE_DB.External_Stages.AWS_Stage
url = 's3:bucketsnowflake3' -- Packet is stored here.
credentials = (aws_key_id='ABCD_DUMMY_ID' aws_secret_key='123abc_key');

-- Description of external stage:
DESC STAGE MANAGE_DB.External_Stages.AWS_Stage;

-- Alter external stage:
ALTER STAGE AWS_Stage
SET credentials=(aws_key_id='XYZ_DUMMY_ID' aws_secret_key='789xyz');

-- Publically accessible staging area:
CREATE OR REPLACE STAGE Manage_DB.External_Stages.AWS_Stage
url = 's3://bucketsnowflake3';

-- List files in stage:
LIST @AWS_Stage;
```

### Loading data from stage to table

```sql
# Create table:
CREATE OR REPLACE TABLE DatabaseName.SchemaName.TableName (
Order_ID VARCHAR(30),
Amount INT,
Profit INT,
Quantity INT,
Category VARCHAR(30),
Subcategory VARCHAR(30));

SELECT * FROM DatabaseName.SchemaName.TableName

-- Copy from stage to table:
COPY INTO DatabaseName.SchemaName.TableName
FROM @Manage_DB.External_Stages.AWS_Stage
file_format = (type=csv field_delimiter=',' skip_header=1)
files = ('OrderDetails.csv'); -- pattern = '*.csv*'
```

### Transforming using SELECT statement

```sql
COPY INTO DatabaseName.SchemaName.TableName 
FROM (SELECT S.C1, S.C2 FROM @MANAGE_DB.EXTERNAL_STAGES.AWS_STAGE S)
file_format = (type=csv field_delimiter=',' skip_header=1)
files = ('OrderDetails.csv'); 
```
