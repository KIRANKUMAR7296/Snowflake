# Warehouse

### What is Data Warehouse?

- Data warehouse `consolidates` and `integrates` different data sources and use them for `reporting` and `data analysis`
- Basically is a database that combines different types of data (Structured, unstructured, relational) from different data sources.
- Data is extracted from different data sources, data is transformed (clean and improve the quality) and then loaded in the warehouse.

### Cloud Computing

- It is necessary to have data centers if the company or organization wants to work with data.
- It can cause lots of overhead i.e pysically available building, infrastructure, security, lot of electricity for cooling, software and hardware updates.
- Managing virtual machines and all the servers and databases (SaaS)
- Therefore all of the overhead is outsourced and then the company can only focus on the actual business by creating there own warehouse.

### Snowflake is a Saas

1. `Application` (We can only focus on creating warehouse, database, schema and tables)
2. `Software`, `Data` and `OS` is handled by Snowflake (Managing data storage, virtual warehouses, upgrades and metadata)
3. `Physical Servers`, `Virtual Machines` and `Physical Storage` are provided by cloud providers i.e AWS, GCP or Azure.

```SQL
DROP WAREHOUSE IF EXISTS WarehouseName

CREATE WAREHOUSE IF NOT EXISTS WarehouseName
WITH WAREHOUSE_SIZE = 'XSMALL'
WAREHOUSE_TYPE = 'STANDARD'
AUTO_SUSPEND = 600 -- In seconds i.e. 10 minutes.
AUTO_RESUME = TRUE 
MIN_CLUSTER_COUNT = 1
MAX_CLUSTER_COUNT = 3
SCALING_POLICY = 'STANDARD'
COMMENT = 'This warehouse is for learning purpose'
```
