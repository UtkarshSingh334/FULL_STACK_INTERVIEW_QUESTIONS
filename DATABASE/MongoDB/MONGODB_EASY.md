# 🍃 MongoDB - Easy Questions

> **Topics Covered:** What is MongoDB, SQL vs NoSQL Differences, BSON vs JSON, Collections and Documents, Basic CRUD Operations (`insertOne`, `find`, `updateOne`, `deleteOne`), Common Query Operators (`$gt`, `$in`, `$set`).

---

### Q1: What is MongoDB and SQL vs NoSQL?
**Question:** What is MongoDB? Compare SQL (Relational) and NoSQL (Document) databases.

**Answer:**
- **MongoDB** is a source-available, cross-platform, document-oriented NoSQL database that stores data in flexible, JSON-like **BSON (Binary JSON)** documents.
- **SQL vs NoSQL Comparison:**
  | Feature | SQL (MySQL, PostgreSQL) | NoSQL (MongoDB) |
  | :--- | :--- | :--- |
  | **Data Model** | Relational tables with fixed columns and rows | Collections of flexible BSON documents |
  | **Schema** | Rigid, predefined schema | Dynamic, flexible schema per document |
  | **Relationships** | Foreign Keys and `JOIN` operations | Embedded Subdocuments or Document References (`$lookup`) |
  | **Scaling** | Vertical scaling (Scale-up CPU/RAM) | Horizontal scaling (Scale-out Sharding) |
  | **Transactions** | ACID compliant by default | ACID transactions supported across collections |

---

### Q2: Basic CRUD Operations in MongoDB
**Question:** Write MongoDB shell commands for Create, Read, Update, and Delete operations.

**Answer:**
```javascript
// 1. Create (Insert)
db.users.insertOne({ name: "Utkarsh Singh", email: "utkarsh@example.com", age: 24, skills: ["Node.js", "React"] });

// 2. Read (Query with operators)
db.users.find({ age: { $gte: 18 }, skills: { $in: ["React"] } }).sort({ age: -1 }).limit(10);

// 3. Update (Using $set and $push)
db.users.updateOne(
  { email: "utkarsh@example.com" },
  { $set: { status: "active" }, $push: { skills: "MongoDB" } }
);

// 4. Delete
db.users.deleteOne({ email: "utkarsh@example.com" });
```
