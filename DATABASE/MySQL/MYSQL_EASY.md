# 🐬 SQL & Relational Databases - Questions From Notes

> **Topics from Notes Covered:** SQL vs NoSQL, Why use SQL (SQL Reasons), Indexing in SQL.

---

### Q1: Why Use SQL & Relational Databases? (SQL Reasons)
**Question (From Notes):** What are the primary reasons to use SQL over NoSQL?

**Answer:**
1. **Strict ACID Guarantees**: Complete transactional reliability for critical operations (payments, inventory, banking).
2. **Normalized Schemas**: Prevents data duplication through Primary/Foreign Key relations.
3. **Complex Joins**: Supports multi-table relational queries via standard SQL.
4. **Standardized Language**: Universal declarative query syntax supported by all enterprise tools.

---

### Q2: Indexing in SQL Databases
**Question (From Notes):** How does indexing work in SQL databases?

**Answer:**
SQL indexes build a B-Tree structure over table columns to allow $O(\log N)$ search time instead of a full table scan.

```sql
-- Single-column index
CREATE INDEX idx_user_email ON users(email);

-- Compound index (ESR rule)
CREATE INDEX idx_orders_status_date ON orders(status, created_at);
```
