# 🍃 MongoDB - Advanced / Hard Questions

> **Topics Covered:** Replica Sets & High Availability (Primary, Secondary, Arbiter, Oplog, Elections), Sharding Architecture (Mongos, Config Servers, Shard Keys), ACID Multi-Document Transactions, WiredTiger Storage Engine & Concurrency Locking.

---

### Q1: MongoDB Replication Architecture (Replica Sets)
**Question:** How do MongoDB Replica Sets provide high availability and automatic failover?

**Answer:**
- A **Replica Set** is a cluster of MongoDB instances that maintain the same data copy.
- **Components:**
  1. **Primary Node**: Receives all write operations. Writes are recorded in the **Oplog (Operations Log)**.
  2. **Secondary Nodes**: Replicate the Primary's Oplog asynchronously and apply changes locally. Can serve read queries (`readPreference: 'secondary'`).
  3. **Arbiter Node** (Optional): Holds no data; participates in elections to break ties.
- **Automatic Failover**: If the Primary fails or becomes unreachable for >10 seconds, secondaries hold an election using the Raft-like consensus algorithm to elect a new Primary.

---

### Q2: MongoDB Sharding (Horizontal Partitioning)
**Question:** Explain MongoDB Sharding architecture. What is a Shard Key and how do you choose an optimal one?

**Answer:**
- **Sharding** distributes collection data across multiple physical machines to support massive datasets and high throughput.
- **Architecture Components:**
  - **`mongos` (Query Router)**: Acts as the entry point; routes client queries to appropriate shards.
  - **Config Servers**: Store cluster metadata and chunk routing tables.
  - **Individual Shards**: Each shard is a replica set holding a subset of sharded data chunks.
- **Shard Key Selection Criteria:**
  - Must have **high cardinality** (many unique values).
  - Even write distribution (avoid monotonic increasing keys like timestamps which cause hotspotting on a single shard).
