# 🍃 MongoDB - Top 10 Practical Coding Queries

> **Practical Interview Queries:** Filtering, Grouping, Join with `$lookup`, Sales calculations, Duplicate finding, Top N salaries, and Index creation.

---

### 1. Find Users Older than 18
```javascript
db.users.find({ age: { $gt: 18 } });
```

---

### 2. Find Users from a Particular State (e.g. "California")
```javascript
db.users.find({ "address.state": "California" });
```

---

### 3. Sort Users by Age (Descending)
```javascript
db.users.find().sort({ age: -1 });
```

---

### 4. Count Users by City
```javascript
db.users.aggregate([
  {
    $group: {
      _id: "$city",
      totalUsers: { $sum: 1 }
    }
  },
  { $sort: { totalUsers: -1 } }
]);
```

---

### 5. Find Duplicate Emails in a Collection
```javascript
db.users.aggregate([
  {
    $group: {
      _id: "$email",
      count: { $sum: 1 },
      docs: { $push: "$_id" }
    }
  },
  {
    $match: {
      count: { $gt: 1 }
    }
  }
]);
```

---

### 6. Find Top 5 Highest-Paid Employees
```javascript
db.employees.find().sort({ salary: -1 }).limit(5);
```

---

### 7. Join Users and Orders Using `$lookup`
```javascript
db.orders.aggregate([
  {
    $lookup: {
      from: "users",
      localField: "userId",
      foreignField: "_id",
      as: "customer"
    }
  },
  { $unwind: "$customer" }
]);
```

---

### 8. Calculate Total Sales and Average Order Value by Category
```javascript
db.orders.aggregate([
  { $match: { status: "completed" } },
  {
    $group: {
      _id: "$category",
      totalSales: { $sum: "$amount" },
      avgOrderValue: { $avg: "$amount" },
      orderCount: { $sum: 1 }
    }
  },
  { $sort: { totalSales: -1 } }
]);
```

---

### 9. Find the Second-Highest Salary in MongoDB
```javascript
db.employees.find({}, { salary: 1, _id: 0 })
  .sort({ salary: -1 })
  .skip(1)
  .limit(1);
```

---

### 10. Create a Compound Index on Status and CreatedAt
```javascript
db.orders.createIndex({ status: 1, createdAt: -1 });
```
