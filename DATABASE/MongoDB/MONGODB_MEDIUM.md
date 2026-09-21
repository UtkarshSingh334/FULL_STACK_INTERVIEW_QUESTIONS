# 🍃 MongoDB - Medium & Aggregation Pipeline

> **Topics Covered:** Types of MongoDB Indexes (Single-Field, Compound, Multikey, Text, Unique, Sparse, TTL), The Aggregation Pipeline (`$match`, `$group`, `$project`, `$lookup`, `$unwind`), `find()` vs Aggregation, Mongoose `populate()` vs `$lookup`, MongoDB ACID Transactions, Replica Sets & Sharding, Query Optimization with `explain()`.

---

### Q1: The 7 Core Index Types in MongoDB ⭐⭐⭐
**Question:** Explain the most common MongoDB index types and options.

**Answer:**
1. **Single-Field Index**: Indexes a single field (`db.users.createIndex({ email: 1 })`).
2. **Compound Index**: Indexes multiple fields. Field order is critical (Follows Left-Prefix rule).
3. **Multikey Index**: Created automatically when indexing an array field (indexes every element).
4. **Text Index**: Provides full-text word search capabilities across string content.
5. **TTL (Time-To-Live) Index**: Automatically removes documents after a set time threshold (great for OTPs and sessions):
   ```javascript
   db.sessions.createIndex({ createdAt: 1 }, { expireAfterSeconds: 3600 });
   ```
6. **Unique Index**: Enforces uniqueness on the indexed field:
   ```javascript
   db.users.createIndex({ email: 1 }, { unique: true });
   ```
7. **Sparse Index**: Only indexes documents that contain the indexed field, saving storage.

---

### Q2: Aggregation Pipeline Stages (`$match`, `$group`, `$project`, `$lookup`, `$unwind`) ⭐⭐⭐
**Question:** Explain the 5 core stages of the MongoDB Aggregation Pipeline with code examples.

**Answer:**
1. **`$match`**: Filters documents to pass only matching documents to the next stage.
2. **`$group`**: Groups input documents by a specified `_id` key and applies accumulators (`$sum`, `$avg`, `$min`, `$max`).
3. **`$project`**: Reshapes documents (includes/excludes fields or computes new computed fields).
4. **`$lookup`**: Performs a Left Outer Join with another collection in the same database.
5. **`$unwind`**: Deconstructs an array field from input documents to output a document for each element.

```javascript
db.orders.aggregate([
  { $match: { status: "Delivered" } },
  {
    $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "user"
    }
  },
  { $unwind: "$user" },
  {
    $group: {
      _id: "$user.city",
      totalRevenue: { $sum: "$totalAmount" },
      orderCount: { $sum: 1 }
    }
  },
  { $sort: { totalRevenue: -1 } }
]);
```

---

### Q3: `find()` vs Aggregation & Mongoose `populate()` vs `$lookup`
**Question:** When should you use `find()` vs `aggregate()`? Compare Mongoose `populate()` with MongoDB `$lookup`.

**Answer:**
- **`find()` vs `aggregate()`**:
  - `find()` is for simple filtering, pagination, and projection on a single collection.
  - `aggregate()` is for multi-stage data transformation, grouped calculations, joins, and analytical reporting.
- **`populate()` vs `$lookup()`**:
  - **`populate()`**: Performed at the **Application/Node.js level** by Mongoose by firing secondary queries behind the scenes.
  - **`$lookup()`**: Executed natively **inside the MongoDB Database Engine** in a single optimized database operation.

---

### Q4: How Do You Optimize a Slow MongoDB Query?
**Question:** How do you profile and optimize slow queries using `explain()`?

**Answer:**
1. Append `.explain("executionStats")` to your query.
2. Check `winningPlan.stage`:
   - `COLLSCAN` (Collection Scan): **Bad**. Scanned every document in the collection.
   - `IXSCAN` (Index Scan): **Good**. Used a B-Tree index.
3. Compare `totalDocsExamined` vs `nReturned`. If `totalDocsExamined` $\gg$ `nReturned`, an index is missing or suboptimal.
4. Create compound indexes matching the **ESR Rule** (Equality $ightarrow$ Sort $ightarrow$ Range).
