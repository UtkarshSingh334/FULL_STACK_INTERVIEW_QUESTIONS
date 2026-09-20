# 🍃 Database & Cache - Hard Questions From Notes

> **Topics from Notes Covered:** Redis Use Cases & Why It is Not Used in Most Projects, Index Execution Performance.

---

### Q1: Redis Use Cases and Why It is NOT Used in Most Projects
**Question (From Notes):** What are the primary Redis use cases, and why is Redis not used in most small/medium projects?

**Answer:**
**Primary Redis Use Cases:**
1. **In-Memory Caching**: Caching expensive database query results with TTL expiration.
2. **Session Store**: Shared session storage across distributed, load-balanced Node servers.
3. **Rate Limiting**: Atomic counter increments (`INCR`, `EXPIRE`) for API throttles.
4. **Pub/Sub & Message Queues**: Background worker job scheduling (BullMQ).
5. **Distributed Locks**: Coordinating concurrency across microservices using Redlock algorithm.

**Why Redis is NOT Used in Most Projects:**
1. **RAM Cost**: Redis stores data completely in RAM, which is significantly more expensive per GB than SSD/NVMe disk storage.
2. **Architectural Complexity**: Introduces cache invalidation challenges, cache stampedes, and cache penetration problems.
3. **Data Volatility Risk**: As an in-memory store, it is not a primary durable ACID database (though it has RDB/AOF persistence).
4. **Maintenance Overhead**: Requires dedicated cluster management, memory eviction policies (`LRU`/`LFU`), and failover configuration.
5. **Premature Optimization**: Most small/medium projects never reach traffic levels where standard database indexing is insufficient.
