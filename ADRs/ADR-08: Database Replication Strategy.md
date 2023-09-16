## ADR-08: Database Replication Strategy

### Status
Adopted

### Context
Given the nature of our platform, which is expected to scale to handle millions of users worldwide, data integrity, high availability, and read-write operations efficiency are paramount. Replicating our database is a strategy that ensures data availability and load distribution. There are various replication strategies, including:

1. **Primary-Read Replica Replication**:
    - All write operations are performed on the primary node, while read operations can be distributed among one or more read replicas.
    - Provides a mechanism for backup, read scalability, and can serve as a failover.
    - However, if the primary fails, a read replica needs to be promoted, and there might be a downtime or data inconsistency during this period.

2. **Multi-Primary Replication**:
    - Multiple nodes (or primaries) can handle both read and write operations.
    - More complex than Primary-Read Replica, as it requires conflict resolution mechanisms when the same data is modified differently in two nodes.
    - Suitable for systems where write availability and distributed writes are essential.

3. **Sharding**:
    - Data is split, or "sharded", and each unique shard is held on a separate database.
    - Scales horizontally, but adds application and operational complexity as data isn’t located in a single place.

Given our application's requirements and growth trajectory, and balancing complexity, we had to decide on an optimal strategy.

### Decision
We have decided to go with **Primary-Read Replica Replication** for the following reasons:

1. **Simplicity**: Primary-Read Replica is relatively simple to set up compared to multi-primary and sharding.
2. **Read Scalability**: With our user base growing, the ability to offload read operations to multiple read replicas will be crucial for performance.
3. **Backup**: Read replicas can serve as an automatic backup mechanism. If the primary goes down, one of the read replicas can be promoted to primary, ensuring data integrity.
4. **Cost**: It offers a balanced cost for setup, maintenance, and scalability.

### Consequences
**Pros**:
- **Efficient Read Operations**: With multiple read replicas, read operations can be distributed, allowing for faster data access.
- **Data Redundancy**: Data is stored in multiple locations, reducing chances of total data loss.
- **Failover Mechanism**: In case the primary fails, a read replica can take over, minimizing downtime.

**Cons**:
- **Write Bottleneck**: All write operations are directed to the primary, which could be a bottleneck when there are many concurrent write operations.
- **Latency in Data Propagation**: There can be a slight delay in data propagation from the primary to the read replicas.
- **Manual Intervention**: If the primary fails, promoting a read replica might require manual intervention or a well-configured automated system.