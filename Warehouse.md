# Warehouse

### What is Data Warehouse?

- Data warehouse `consolidates` and `integrates` different data sources and use them for `reporting` and `data analysis`
- Basically is a database that combines different types of data (Structured, unstructured, relational) from different data sources.
- Data is extracted from different data sources, data is transformed (clean and improve the quality) and then loaded in the warehouse.
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
