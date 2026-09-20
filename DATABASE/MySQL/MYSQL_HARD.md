# 🐬 MySQL - Hard Interview Questions & Solutions

---

### Q1: InnoDB Storage Engine: Clustered vs Secondary Indexes
**Answer:**
- **Clustered Index**: The table rows are stored physically on disk sorted by the **Primary Key**. The leaf nodes of the B+ Tree contain the **actual row data**. A table can have only ONE Clustered Index.
- **Secondary Index**: Leaf nodes do NOT store the entire row; they store the indexed column values and a pointer to the **Primary Key value**.
- **Double Lookup**: Querying via a secondary index first searches the secondary B+ tree to find the Primary Key, then performs a lookup in the Clustered Index B+ tree (known as **Bookmark Lookup / Index Lookup**).
- **Covering Index**: If all queried columns are present in the secondary index itself, MySQL avoids the secondary lookup entirely.

---

### Q2: Transaction Isolation Levels & Concurrency Anomalies
**Answer:**
| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read |
| :--- | :--- | :--- | :--- |
| **Read Uncommitted** | ❌ Allowed | ❌ Allowed | ❌ Allowed |
| **Read Committed** | ✅ Prevented | ❌ Allowed | ❌ Allowed |
| **Repeatable Read** (MySQL Default) | ✅ Prevented | ✅ Prevented (via MVCC) | ✅ Prevented (via Next-Key Locks) |
| **Serializable** | ✅ Prevented | ✅ Prevented | ✅ Prevented |

- **Dirty Read**: Transaction reads uncommitted changes from another transaction.
- **Non-Repeatable Read**: Transaction re-reads the same row and discovers values have changed.
- **Phantom Read**: Transaction re-runs a range query and discovers new rows inserted by another transaction.

---

### Q3: InnoDB Redo Log (WAL) vs Undo Log (MVCC)
**Answer:**
1. **Redo Log (Write-Ahead Logging / WAL)**: Ensures **Durability (D in ACID)**. When data changes, it writes sequentially to the Redo Log buffer on disk before dirty pages are flushed to actual data files. Allows crash recovery upon unexpected reboot.
2. **Undo Log**: Ensures **Atomicity (A)** and **Isolation (I)**. Stores previous versions of records so transactions can rollback changes, and powers **Multi-Version Concurrency Control (MVCC)** so reading transactions never block writing transactions.
