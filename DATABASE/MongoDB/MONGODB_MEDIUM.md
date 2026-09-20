# 🍃 Database & MongoDB - Medium Questions From Notes

> **Topics from Notes Covered:** Populate (in DB), Query in Populate, Compound Indexing, Inbound Indexing.

---

### Q1: Populate in DB (Mongoose `populate`)
**Question (From Notes):** What is `populate()` in MongoDB/Mongoose and how does it work under the hood?

**Answer:**
Because MongoDB does not natively support relational SQL `JOIN`s, Mongoose `populate()` replaces specified document ID references with the actual documents from referenced collections by performing a secondary `$in` batch query behind the scenes in Node.js application memory.

```javascript
const User = require('../models/User');

async function getUserProfile(userId) {
  return await User.findById(userId).populate('profile').exec();
}
```

---

### Q2: Query in Populate (Filtering, Sorting, and Projections Inside Populate)
**Question (From Notes):** How do you filter, sort, and limit query results inside `populate()`?

**Answer:**
```javascript
async function getDeliveredOrders(userId) {
  return await User.findById(userId)
    .populate({
      path: 'orders',
      match: { status: 'DELIVERED', amount: { $gte: 100 } }, // Query filter inside populated model
      select: 'orderNumber amount createdAt items',
      options: { sort: { createdAt: -1 }, limit: 5 },
      populate: {
        path: 'items.product', // Nested populate
        select: 'name price'
      }
    })
    .exec();
}
```

---

### Q3: Compound Indexing vs Single-Field (Inbound) Indexing & The ESR Rule
**Question (From Notes):** What is Compound Indexing and how does it work?

**Answer:**
- **Single-Field / Inbound Index**: Indexes a single attribute (e.g. `{ email: 1 }`).
- **Compound Index**: Indexes multiple fields together in a single B-Tree structure. The order of fields matters significantly.

**The ESR (Equality, Sort, Range) Rule:**
1. **Equality (E)**: Fields matching exact equality (`status: "ACTIVE"`) go **first**.
2. **Sort (S)**: Fields used for ordering (`sort: { createdAt: -1 }`) go **second**.
3. **Range (R)**: Fields queried with range operators (`$gt`, `$lte`, `$in`) go **last**.

```javascript
// Query: db.orders.find({ status: "PAID", total: { $gte: 500 } }).sort({ createdAt: -1 })
// Optimal Compound Index:
db.orders.createIndex({ status: 1, createdAt: -1, total: 1 });
```
