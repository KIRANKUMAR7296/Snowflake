# Snowflake Architecture

## `Storage`
- First layer is storage (All the data is stored)
- Data is not stored in the Snowflake itself, It is stored in AWS buckets, GCP or Microsoft Azure.
- Data is stored in `Hybrid Columnar Storage` called as `blobs` in compressed form.
- Data is fetched using the queries and we also receive the data in form of blobs.
- Efficient storage and faster querying capability.

## Query Processing (Muscle)
- Second layer where the queries are processed.
- Virtual warehouses are `compute` resource that process all our queries and operations that are performed.
- Also performs massive parallel processing (Multiple users can run seperate worksheets at same time.)

### Virtual Warehouse Sizes

1. `XS`: Only 1 server of small size for Simple queries (If we run complex query it will take more time to execute)
2. `S`: 2 servers
3. `M`: 4 servers
4. `L`: 8 servers
5. `XL`: 16 servers
6. `4XL`: 128 servers (Most expensive)

### Multi Clustering (Brain)
- `Multi clustering` is possible in `enterprise` versions (Especially designed for small or large scale organizations)
- N number of users can run n number of queries at same instance of time in fraction of seconds or minutes.

## `Cloud Services`
- Third layer were all the management happens.
- Managing infrastructure, access allocation, security, query optimization, updating metadata, etc
