# 🍃 MongoDB - Medium Questions

> **Topics Covered:** Complete Guide to MongoDB Indexing (All 9 Types) ⭐⭐⭐, Index Options (`unique`, `sparse`, `partialFilterExpression`, TTL), Aggregation Pipeline (`$match`, `$group`, `$project`, `$lookup`, `$unwind`), Mongoose ODM (`populate`, Schemas, Hooks), Embedded Documents vs References.

---

### Q1: Types of Indexing in MongoDB ⭐⭐⭐
**Question:** Explain all 9 types of Indexes in MongoDB and their options. How do you measure query execution performance?

**Answer:**
Indexes in MongoDB improve query execution speed by creating ordered B-Tree data structures, avoiding costly full collection scans (`COLLSCAN`).

#### 9 Index Types:
1. **Default `_id` Index**: Automatically created unique index on the primary `_id` field.
2. **Single Field Index**: User-defined index on a single document key:
   ```javascript
   db.users.createIndex({ email: 1 }); // 1 = Ascending, -1 = Descending
   ```
3. **Compound Index**: Index on multiple fields (order of fields matters - follows Left-Prefix rule):
   ```javascript
   db.users.createIndex({ status: 1, age: -1 });
   ```
4. **Multikey Index**: Created automatically when an indexed field contains an **array** value (indexes each array element).
5. **Text Index**: Enables full-text search across string fields with word stemming and stop-words:
   ```javascript
   db.articles.createIndex({ title: "text", content: "text" });
   db.articles.find({ $text: { $search: "fullstack javascript" } });
   ```
6. **Geospatial Index (`2dsphere` / `2d`)**: Calculates distances on sphere/flat surface for coordinate queries (`$near`, `$geoWithin`).
7. **Hashed Index**: Hashes field value; used for even partition distribution across shards in MongoDB Sharding.
8. **Wildcard Index**: Indexes all arbitrary or unknown nested dynamic sub-fields (`db.products.createIndex({ "attributes.$**": 1 })`).
9. **Clustered Index**: Stores collection documents directly ordered by clustered index key.

#### Important Index Options:
- **`unique: true`**: Rejects duplicate entries (`db.users.createIndex({ email: 1 }, { unique: true })`).
- **`sparse: true`**: Only indexes documents that contain the indexed field.
- **`expireAfterSeconds` (TTL Index)**: Automatically deletes documents after a duration (ideal for OTPs and sessions).
- **`partialFilterExpression`**: Indexes only documents matching a specific filter condition.

#### Performance Analysis with `explain()`:
```javascript
db.users.find({ email: "test@test.com" }).explain("executionStats");
// Look for stage: "IXSCAN" (Index Scan - Fast) vs "COLLSCAN" (Collection Scan - Slow)
```

---

### Q2: Aggregation Pipeline Deep Dive
**Question:** Explain the MongoDB Aggregation Pipeline with an example of `$match`, `$group`, `$project`, `$sort`, and `$lookup`.

**Answer:**
The Aggregation Framework processes documents through a multi-stage pipeline:

```javascript
db.orders.aggregate([
  // Stage 1: Filter completed orders in 2026
  { $match: { status: "completed", year: 2026 } },

  // Stage 2: Join with users collection (Left Outer Join)
  {
    $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "customerDetails"
    }
  },

  // Stage 3: Unwind joined array
  { $unwind: "$customerDetails" },

  // Stage 4: Group by customer and compute total spend
  {
    $group: {
      _id: "$userId",
      customerName: { $first: "$customerDetails.name" },
      totalSpent: { $sum: "$totalAmount" },
      orderCount: { $sum: 1 }
    }
  },

  // Stage 5: Sort by highest spenders
  { $sort: { totalSpent: -1 } },

  // Stage 6: Project final output fields
  {
    $project: {
      _id: 0,
      userId: "$_id",
      customerName: 1,
      totalSpent: 1,
      orderCount: 1
    }
  }
]);
```

---

### Q3: Mongoose `populate()` vs Embedded Documents
**Question:** When should you embed subdocuments versus reference documents with Mongoose `populate()`?

**Answer:**
- **Embedding (Denormalization)**:
  - *When to use:* 1-to-1 or 1-to-Few relationships where child data is always retrieved together with the parent (e.g., User addresses, Order line items).
  - *Advantage:* Fast single-document reads without joining.
- **Referencing (Normalization with `populate`)**:
  - *When to use:* 1-to-Many or Many-to-Many relationships where child documents grow unboundedly or are queried independently (e.g., Users $\leftrightarrow$ Posts $\leftrightarrow$ Comments).

```javascript
// Mongoose Populate Example
const PostSchema = new mongoose.Schema({
  title: String,
  author: { type: mongoose.Schema.Types.ObjectId, ref: 'User' }
});

const post = await Post.findById(postId).populate('author', 'name email');
```
