# Warehouse

### What is Data Warehouse?

- Purpose of a data warehouse is to `consolidate` and `integrate` different data sources and use them for `reporting` and `data analysis`

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
