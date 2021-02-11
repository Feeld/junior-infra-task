# Checks

### HTTP API

- Health checks (200 OK)
- Inverse health checks (not 200 OK)
- Requests per minute
- Errors per minute

### PostgreSQL

- Number of sequential scans on a table
- Number of index scans on a table
- Rows fetched vs returned by queries to the database
- Rows inserted, updated, deleted by queries (per table or per database)
- Replication delay
- Number of active connections
- Percentage of max connections in use
- Max time a client connection has been waiting to be served

### Redis

- Latency
- Hit rate
- Used memory
- Connected clients
- Connected replicas
- Last interaction with primary (seconds)
- Last save time

### RabbitMQ

- Messages in
- Messages out
- Messages unroutable
- Node disk space used
- Node memory used
- File descriptors used
- Data rates
- Queue count
- Message rates
- Number of consumers

### MongoDB

- Number of read requests received during the selected time period
- Number of write requests received during the selected time period
- Number of clients with read operations in progress or queued
- Number of clients with write operations in progress or queued
- Number of read requests currently queued
- Number of write requests currently queued
- Size of the oplog
- Oplog window
- Replication lag
- Number of clients currently connected to the database server
- Number of unused connections available for new clients
- Number of message assertions
- Number of warning assertions
- Number of regular assertions