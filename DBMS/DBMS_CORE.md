# 🗄️ DBMS & Database Architecture Core

> **Topics Covered:** DBMS vs RDBMS, Keys (Primary, Foreign, Candidate, Composite), Database Normalization (1NF, 2NF, 3NF, BCNF) & Denormalization, ACID Properties of Transactions, Clustered vs Non-Clustered Indexes, Views, Stored Procedures, Triggers, Deadlocks & Prevention, Concurrency & Transaction Isolation Levels, SQL Injection.

---

### Q1: DBMS vs RDBMS & Database Keys Explained
**Question:** Compare DBMS and RDBMS. Explain Primary Key, Foreign Key, Candidate Key, and Composite Key.

**Answer:**
- **DBMS**: General system for storing data in files/records (flat files, hierarchical).
- **RDBMS**: Relational DBMS (MySQL, PostgreSQL, Oracle) that stores data in tables with relationships, enforcing ACID constraints and relational integrity.
- **Database Keys:**
  1. **Candidate Key**: A set of one or more columns that can uniquely identify a table record.
  2. **Primary Key**: The chosen candidate key that uniquely identifies each row (Cannot contain NULL).
  3. **Foreign Key**: A column in one table referencing the Primary Key of another table, establishing a relationship.
  4. **Composite Key**: A primary key made up of **two or more columns combined** together.

---

### Q2: Database Normalization (1NF, 2NF, 3NF, BCNF) vs Denormalization ⭐⭐⭐
**Question:** Explain 1NF, 2NF, 3NF, and BCNF. Why and when would you denormalize a database?

**Answer:**
- **1NF (First Normal Form)**: All column values must be **atomic** (indivisible; no comma-separated arrays). Each record must have a unique identifier.
- **2NF (Second Normal Form)**: Must be in 1NF. **No Partial Dependencies** (Every non-key attribute must depend on the *entire* primary key, not just a part of a composite key).
- **3NF (Third Normal Form)**: Must be in 2NF. **No Transitive Dependencies** ($A ightarrow B ightarrow C$; non-key column cannot depend on another non-key column).
- **BCNF (Boyce-Codd Normal Form)**: Stricter 3NF. For every functional dependency $X ightarrow Y$, $X$ must be a **Super Key**.
- **Denormalization**: Intentionally introducing controlled redundancy into a normalized database to reduce expensive multi-table `JOIN` operations and speed up read-heavy queries in data warehouses or high-traffic reporting dashboards.

---

### Q3: Transaction Isolation Levels & Concurrency Anomalies
**Question:** Explain the 4 SQL Transaction Isolation Levels and the 3 concurrency read phenomena they prevent.

**Answer:**
- **Concurrency Read Phenomena:**
  1. **Dirty Read**: Transaction A reads uncommitted data written by Transaction B (which might later be rolled back).
  2. **Non-Repeatable Read**: Transaction A reads a row, Transaction B updates that row and commits; Transaction A re-reads the row and sees different values.
  3. **Phantom Read**: Transaction A queries a range of rows, Transaction B inserts new rows matching that range and commits; Transaction A re-queries and sees "phantom" rows.

| Isolation Level | Dirty Read | Non-Repeatable Read | Phantom Read | Performance |
| :--- | :--- | :--- | :--- | :--- |
| **Read Uncommitted** | ⚠️ Allowed | ⚠️ Allowed | ⚠️ Allowed | Fastest |
| **Read Committed** | ❌ Prevented | ⚠️ Allowed | ⚠️ Allowed | Standard Default |
| **Repeatable Read** | ❌ Prevented | ❌ Prevented | ⚠️ Allowed (Prevented in MySQL InnoDB via Next-Key Locks) | High |
| **Serializable** | ❌ Prevented | ❌ Prevented | ❌ Prevented | Slowest (Locks Range) |

---

### Q4: Database Deadlocks & Prevention
**Question:** What is a Deadlock in a database? How does the database detect and resolve it?

**Answer:**
- **Deadlock**: A situation where Transaction 1 holds a lock on Row A and waits for Row B, while Transaction 2 holds a lock on Row B and waits for Row A. Neither can proceed.
- **Resolution**:
  - The RDBMS deadlock detector builds a **Wait-For Graph**.
  - When a cycle is detected, the engine automatically selects the cheaper transaction (victim) and rolls it back, releasing locks for the other transaction.
- **Prevention Best Practices**:
  1. Access database tables and rows in the exact same consistent order across all application code.
  2. Keep transactions short and commit promptly.
