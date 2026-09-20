# 🍃 Database & MongoDB - Easy Questions From Notes

> **Topics from Notes Covered:** NoSQL vs SQL, SQL Reasons, Database Indexing Basics.

---

### Q1: NoSQL vs SQL & SQL Reasons
**Question (From Notes):** What is the difference between NoSQL and SQL? What are the reasons to choose SQL over NoSQL?

**Answer:**
| Feature | SQL (Relational: PostgreSQL, MySQL) | NoSQL (Document: MongoDB) |
| :--- | :--- | :--- |
| **Schema** | Fixed, rigid tabular schema | Dynamic, flexible BSON/JSON schema |
| **Relationships** | Complex foreign key `JOIN`s | Embedded subdocuments or `$lookup`/`populate` |
| **Scaling** | Vertical scaling (bigger CPU/RAM) | Horizontal scaling (Sharding) |
| **Transactions** | Full ACID compliance out of the box | Document-level atomicity, multi-doc ACID via sessions |

**Reasons to choose SQL:**
1. **Strict Data Integrity**: When schemas must adhere strictly to constraints (banking, financial ledgers).
2. **Complex Relational Joins**: When data requires deep, multi-table joins.
3. **Standardized Query Language**: Universal standard for analytics and reporting.

---

### Q2: What is Database Indexing?
**Question (From Notes):** What is an Index in a database?

**Answer:**
Without an index, the database must perform a **Full Collection/Table Scan** ($O(N)$), reading every document on disk. An index creates a sorted **B-Tree** data structure holding field values and disk pointers, reducing lookup time to $O(\log N)$.

```javascript
// Create single-field index on email in MongoDB
db.users.createIndex({ email: 1 });
```
