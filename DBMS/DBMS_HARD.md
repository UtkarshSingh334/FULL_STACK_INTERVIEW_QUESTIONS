# 🗄️ DBMS - Questions From Notes (Hard)

> **Topics from Notes Covered:** Redis Use Cases & Why It is Not Used in Most Projects, Advanced Compound Indexing Selectivity.

---

### Q1: Redis Caching Architecture vs Primary Databases
**Question (From Notes):** What are Redis use cases and why is it not used in most projects?

**Answer:**
**Use Cases:**
1. In-memory query caching with TTL.
2. Fast session storage and authentication token blacklist.
3. Distributed locks and rate limiting counters.

**Why Not Used in Most Projects:**
1. **High RAM Cost**: In-memory storage is significantly more expensive than SSD disks.
2. **Cache Invalidation & Consistency Overhead**: Introduces data sync complexity between DB and Cache.
3. **Volatility**: Primary persistence is better handled by ACID databases.

---

### Q2: Compound Index Selectivity & ESR Execution
**Question (From Notes):** How does index selectivity affect compound indexing performance?

**Answer:**
High-selectivity columns (columns with many unique values, like `user_id` or `email`) should be prioritized over low-selectivity columns (like `gender` or `is_active`) to discard non-matching rows as early as possible in the B-Tree traversal.
