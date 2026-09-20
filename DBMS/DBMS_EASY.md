# 🗄️ DBMS - Questions From Notes (Easy)

> **Topics from Notes Covered:** SQL vs NoSQL, Reasons to use SQL.

---

### Q1: SQL vs NoSQL
**Question (From Notes):** What is the difference between SQL (Relational) and NoSQL (Document/MongoDB) databases?

**Answer:**
| Feature | SQL (PostgreSQL, MySQL) | NoSQL (MongoDB) |
| :--- | :--- | :--- |
| **Schema** | Rigid, predefined tabular schema | Flexible, dynamic JSON/BSON documents |
| **Relationships** | Enforced via Foreign Keys & Relational `JOIN`s | Embedded documents or Application-level references (`populate`) |
| **Scaling** | Primarily Vertical Scaling | Horizontal Scaling via Sharding |
| **Data Integrity** | Strict ACID guarantees | Tunable Consistency (Eventual or Strong) |

---

### Q2: Reasons to Use SQL (SQL Reason)
**Question (From Notes):** Why do projects choose SQL over NoSQL?

**Answer:**
1. **Financial & Transactional Integrity**: Strict ACID compliance out of the box.
2. **Complex Queries**: Native multi-table relational `JOIN`s.
3. **Data Normalization**: Eliminates data duplication through normalized tables.
4. **Standardized Ecosystem**: Universal query language.
