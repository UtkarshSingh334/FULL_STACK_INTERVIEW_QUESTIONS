# 📜 JavaScript - Hard Questions From Notes

> **Topics from Notes Covered:** Consoling `this` Keyword across all execution contexts, All Promise Combinators (`Promise.all`, `Promise.allSettled`, `Promise.race`, `Promise.any`).

---

### Q1: Consoling `this` Keyword Across Execution Contexts
**Question (From Notes):** What is output when consoling `this` across different JavaScript execution contexts?

**Answer:**
`this` is evaluated dynamically based on the execution context:

```javascript
// 1. Global Context
console.log(this); 
// In Browser: window
// In Node.js: module.exports (empty object {})

// 2. Regular Function Call
function checkThis() {
  console.log(this);
}
checkThis(); // Non-strict mode: global window | Strict mode ('use strict'): undefined

// 3. Object Method (Implicit Binding)
const profile = {
  name: "Utkarsh",
  show() {
    console.log(this.name);
  }
};
profile.show(); // "Utkarsh" (Bound to profile object)

const extracted = profile.show;
// extracted(); // undefined or TypeError (Lost implicit binding)

// 4. Explicit Binding (call / apply / bind)
function greet() {
  console.log(this.title);
}
greet.call({ title: "Lead Engineer" }); // "Lead Engineer"

// 5. Constructor Call (new keyword)
function User(name) {
  this.name = name;
  console.log(this); // User instance { name: "Sara" }
}
const u = new User("Sara");

// 6. Arrow Function (Lexical Binding)
const team = {
  department: "Tech",
  members: ["Dev1", "Dev2"],
  printTeam() {
    this.members.forEach((m) => {
      // Arrow function captures 'this' lexically from printTeam (the team object)
      console.log(`${m} in ${this.department}`);
    });
  }
};
team.printTeam();
```

---

### Q2: All Promise Combinators (`Promise.all`, `Promise.allSettled`, `Promise.race`, `Promise.any`)
**Question (From Notes):** Compare all Promise combinator methods.

**Answer:**
1. **`Promise.all([p1, p2])`**:
   - Resolves when **all** promises resolve.
   - Rejects immediately (fails fast) if **any single promise rejects**.
2. **`Promise.allSettled([p1, p2])`**:
   - Never rejects early.
   - Waits for all promises to finish and returns an array of outcome objects: `{ status: 'fulfilled', value }` or `{ status: 'rejected', reason }`.
3. **`Promise.race([p1, p2])`**:
   - Settles (resolves or rejects) as soon as the **first promise settles**.
4. **`Promise.any([p1, p2])`**:
   - Resolves as soon as the **first promise fulfills** (ignores rejections unless all reject with `AggregateError`).
