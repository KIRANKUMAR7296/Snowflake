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
