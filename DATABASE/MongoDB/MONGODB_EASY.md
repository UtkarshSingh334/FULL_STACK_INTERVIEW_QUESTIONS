# 🍃 MongoDB - Easy & Core Concepts

> **Topics Covered:** What is MongoDB, MongoDB vs MySQL (NoSQL vs SQL), What is BSON?, BSON vs JSON, Collections and Documents, The `_id` Field & `ObjectId` Structure, Embedded Documents vs References (When to Embed vs When to Reference).

---

### Q1: What is MongoDB and How Does It Differ from MySQL?
**Question:** What is MongoDB? Compare MongoDB with relational SQL databases like MySQL.

**Answer:**
- **MongoDB** is a document-oriented NoSQL database that stores data in flexible, JSON-like BSON documents within collections.
- **Comparison Table:**
  | Feature | MongoDB (NoSQL) | MySQL (SQL) |
  | :--- | :--- | :--- |
  | **Data Structure** | Collections of BSON documents | Tables with rigid rows and columns |
  | **Schema** | Dynamic / Flexible schema | Strict, predefined schema |
  | **Relationships** | Embedded subdocuments or references | Foreign Keys and `JOIN` clauses |
  | **Scaling Model** | Native horizontal scaling (Sharding) | Vertical scaling (Scale-up CPU/RAM) |
  | **Query Language** | MongoDB Query API (JSON/BSON based) | SQL (Structured Query Language) |

---

### Q2: What is BSON and How is it Different from JSON?
**Question:** What is BSON? Why does MongoDB use BSON instead of standard JSON?

**Answer:**
- **BSON (Binary JSON)** is a binary-encoded serialization format of JSON-like documents.
- **Why MongoDB Uses BSON:**
  1. **Additional Data Types**: Standard JSON only supports strings, numbers, booleans, arrays, objects, and null. BSON adds support for `ObjectId`, `Date`, `Binary Data`, `Decimal128`, and `Int64`.
  2. **Faster Traversal & Parsing**: BSON prefixes fields with their byte lengths and type headers, allowing the database engine to skip past irrelevant fields during queries without parsing the whole document text.

---

### Q3: What is `_id` and What is the Internal Structure of an `ObjectId`?
**Question:** What is the `_id` field? What makes up a 12-byte MongoDB `ObjectId`?

**Answer:**
- The **`_id`** is a mandatory primary key field present on every document in a collection, indexed with a unique index by default.
- **12-Byte `ObjectId` Breakdown:**
  1. **4 Bytes**: Unix timestamp in seconds (provides natural chronological sorting).
  2. **5 Bytes**: Random process identifier unique to the machine and process.
  3. **3 Bytes**: Incrementing counter initialized to a random value.

---

### Q4: Embedded Documents vs Document References
**Question:** What is the difference between Embedding and Referencing in MongoDB? When should you use each?

**Answer:**
- **Embedded Documents (Denormalization)**: Storing related data directly inside parent documents.
  - *Use When:* "Contains" relationship (1-to-1 or 1-to-Few); child data is bounded and almost always accessed with the parent (e.g., User shipping addresses, order line items).
  - *Benefits:* Fast single-disk-read retrieval without joins.
- **Document References (Normalization)**: Storing related documents in separate collections and referencing via `ObjectId`.
  - *Use When:* 1-to-Many or Many-to-Many where child data grows unboundedly or is queried independently (e.g., Authors $\leftrightarrow$ Books $\leftrightarrow$ Reviews).
  - *Benefits:* Prevents hitting the 16MB document size limit and avoids data duplication.
