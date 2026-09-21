# 🗄️ DBMS - Easy & Core Questions

> **Topics Covered:** What is DBMS vs RDBMS, ACID Properties of Database Transactions, Database Normalization (1NF, 2NF, 3NF, BCNF), Primary Key vs Foreign Key vs Unique Key, Clustered vs Non-Clustered Indexes.

---

### Q1: ACID Properties in Database Transactions ⭐⭐⭐
**Question:** Explain the ACID properties with real-world banking transaction examples.

**Answer:**
A transaction is a single logical unit of database work. ACID guarantees data reliability:

1. **Atomicity ("All or Nothing")**:
   - The entire transaction succeeds or is completely rolled back.
   - *Example:* When transferring $500 from Account A to Account B, either both the debit from A and credit to B happen, or neither happens.
2. **Consistency**:
   - The database moves from one valid state to another, upholding all integrity constraints and foreign key rules.
   - *Example:* Total money in bank system remains invariant before and after transfer.
3. **Isolation**:
   - Concurrent transactions execute independently without interfering with or observing intermediate uncommitted states of other transactions.
4. **Durability**:
   - Once a transaction is committed, its changes are permanently recorded on non-volatile storage (disk/WAL), surviving power outages and crashes.

---

### Q2: Database Normalization (1NF, 2NF, 3NF, BCNF) ⭐⭐
**Question:** What is Normalization? Explain 1NF, 2NF, 3NF, and BCNF.

**Answer:**
Normalization is the systematic design process of organizing table schemas to eliminate data redundancy and prevent insertion, update, and deletion anomalies.

- **1NF (First Normal Form)**:
  - Every column must contain **atomic (indivisible) values**.
  - No repeating groups or comma-separated lists in a single cell.
  - Unique primary key identifies each row.
- **2NF (Second Normal Form)**:
  - Must be in 1NF.
  - **No Partial Dependency**: Every non-key attribute must be fully functionally dependent on the primary key (applies to composite primary keys).
- **3NF (Third Normal Form)**:
  - Must be in 2NF.
  - **No Transitive Dependency**: Non-key columns must not depend on other non-key columns ($A ightarrow B ightarrow C$).
- **BCNF (Boyce-Codd Normal Form)**:
  - Stricter version of 3NF. For every functional dependency $X ightarrow Y$, $X$ must be a **Super Key**.

---

### Q3: Clustered Index vs Non-Clustered Index
**Question:** Compare Clustered and Non-Clustered Indexes in Relational Databases.

**Answer:**
| Criteria | Clustered Index | Non-Clustered Index |
| :--- | :--- | :--- |
| **Physical Row Order** | Directly determines the physical storage order of rows on disk | Separate B-Tree index structure pointing to table rows |
| **Count Per Table** | **Only 1** per table (Usually Primary Key) | Multiple allowed per table (e.g. 5-10) |
| **Leaf Nodes** | Contain the actual data pages / rows | Contain index key values and Row Locators (Pointers) |
| **Speed** | Extremely fast for range scans (`BETWEEN`) | Fast for point queries, but requires secondary row lookup |
