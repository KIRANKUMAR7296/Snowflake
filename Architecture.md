# Snowflake Architecture

`Account` > `Database` > `Schema` > `Table`

### `Account`

`Hierarchy` : User | Role | Warehouse | Resource Monitor | Integration | Database | Schema

### `Schema` : A logical grouping of database objects.

`Database Objects` : Table | External Table | View | Stored Procedure | Sequence | Stage | File Format | Pipe | Stream | Task | UDF

## `Storage`
- First layer is storage ( Databases )
- Data is not stored in the Snowflake itself, It is stored in AWS buckets, GCP or Microsoft Azure.
- Data is stored in `Hybrid Columnar Storage` called as `blobs` in compressed form.
- Data is fetched using the queries and we also receive the data in form of blobs.
- Efficient storage and faster querying capability.

## `Query Processing` (Muscle)
- Second layer where the queries are processed.
- `Virtual Warehouses` are `compute` resource that process all our queries and operations that are performed.
- Also performs massive parallel processing (Multiple users can run seperate worksheets at same time.)

### Virtual Warehouse Sizes

In Snowflakes server are considerd as credit per hour.

1. `XS`: Only 1 server of small size for Simple queries (If we run complex query it will take more time to execute)
2. `S`: 2 servers
3. `M`: 4 servers
4. `L`: 8 servers
5. `XL`: 16 servers
6. `2XL`: 32 servers
7. `3XL`: 64 servers
8. `4XL`: 128 servers (Most expensive)

### Multi Clustering (Brain)
- `Multi clustering` is possible in `enterprise` versions (Especially designed for small or large scale organizations)
- N number of users can run n number of queries at same instance of time in fraction of seconds or minutes.

## `Cloud Services`
- Third layer were all the management happens.
- Managing infrastructure, access allocation, security, query optimization, updating metadata, etc

## Scaling Policy

### `Standard` : Default

- Prevents queries from waiting in queues rather it starts additional clusters for running the queries.
- As soon as the system detects that there are more queries that are waiting in the queue it starts another cluster.
- If the cluster is idle it checks the queue for 2 to 3 times and then shut down the clusters.
- Focus on `performance`

### `Economy`

- Conserve server | credits by keeping the running cluster fully loaded and keep the queries to wait in queue for particular time.
- Due to waiting in queue it takes longer time to complete.
- Check the queue 5 to 6 times before closing the cluster.
- Focus on `conservation` of `consumption`
