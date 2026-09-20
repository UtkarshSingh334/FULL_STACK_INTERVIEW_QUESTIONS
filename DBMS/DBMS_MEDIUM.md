# 🗄️ DBMS - Questions From Notes (Medium)

> **Topics from Notes Covered:** Indexing & Types (Single-Field / Inbound Indexing, Compound Indexing), Populate in DB.

---

### Q1: Database Indexing & Types (Single-Field / Inbound vs Compound Indexing)
**Question (From Notes):** Explain Database Indexing, Inbound/Single-Field Indexing, and Compound Indexing.

**Answer:**
- **Index**: A sorted B-Tree data structure enabling $O(\log N)$ search operations instead of full table/collection scans ($O(N)$).
- **Single-Field / Inbound Index**: Indexes a single attribute (e.g. `CREATE INDEX idx_email ON users(email)`).
- **Compound Index**: Indexes multiple attributes together.

**The ESR (Equality, Sort, Range) Rule for Compound Indexing:**
1. **Equality (E)**: Fields matching exact equality queries go **first**.
2. **Sort (S)**: Fields used for ordering go **second**.
3. **Range (R)**: Fields queried with range operators (`$gt`, `$lte`, `BETWEEN`) go **last**.

---

### Q2: Populate in Databases
**Question (From Notes):** How does `populate` work across databases?

**Answer:**
- In SQL, related rows across tables are joined in the database engine using relational `JOIN` operations.
- In NoSQL/MongoDB, `populate` executes an internal secondary query using `$in` to fetch and attach related child documents in application server memory.
