# 📜 JavaScript - Medium & Advanced Concepts

> **Topics Covered:** Lexical Scope vs Dynamic Scope, Scope Chain, IIFE, Execution Context & Call Stack, Closures, Currying vs Partial Application, `this` Binding (`call`, `apply`, `bind`, Arrow Functions), Function Borrowing, Shallow vs Deep Copy, Array Grouping, Sorting, and Flattening, Promises & Combinators, Async/Await Internals, Sequential vs Concurrent Promise Execution.

---

### Q1: Execution Context & The Call Stack ⭐⭐⭐
**Question:** What is an Execution Context in JavaScript? What happens when a function is called?

**Answer:**
An **Execution Context** is an environment in which JavaScript code is evaluated and executed.

#### 2 Types of Execution Context:
1. **Global Execution Context (GEC)**: Created once on startup. Creates `window`/`global` and `this`.
2. **Function Execution Context (FEC)**: Created every time a function is invoked.

#### 2 Phases in Every Execution Context:
1. **Creation (Memory Allocation) Phase**:
   - Variables (`var`) allocated memory and set to `undefined`.
   - `let`/`const` placed in TDZ.
   - Function declarations stored completely in memory.
   - Sets up Scope Chain and `this`.
2. **Execution Phase**:
   - Code runs line-by-line; variables assigned values, functions invoked.

**The Call Stack**: LIFO (Last-In-First-Out) stack structure that manages execution contexts. When a function finishes executing, its context is popped off the stack.

---

### Q2: Lexical Scope vs Dynamic Scope & The Scope Chain
**Question:** What is Lexical Scope? How does it differ from Dynamic Scope? Explain the Scope Chain.

**Answer:**
- **Lexical Scope (Static Scope)**: Scope resolution depends entirely on **where functions and variables are written in the source code at compile time**, NOT where they are called from. JavaScript uses Lexical Scope.
- **Dynamic Scope**: Scope resolution depends on **where the function is called at runtime** (e.g., Bash, older Perl).
- **Scope Chain**: When a variable is referenced, JS searches current local scope $ightarrow$ outer lexical parent scope $ightarrow$ global scope.

```javascript
const x = 10;
function foo() {
  console.log(x); // Lexical: looks at definition site, finds global x = 10
}
function bar() {
  const x = 20;
  foo(); // In dynamic scoping, this would output 20. In JS (lexical), outputs 10!
}
bar(); // Outputs: 10
```

---

### Q3: What is an IIFE (Immediately Invoked Function Expression)?
**Question:** What is an IIFE and why was it heavily used before ES6?

**Answer:**
An **IIFE** is a function that runs immediately upon definition: `(function() { ... })();`.
- **Primary Use Case:** Creating private scopes to prevent polluting the global namespace before ES6 `let`/`const` and modules existed.

```javascript
(function() {
  var privateKey = "12345";
  console.log("IIFE Initialized");
})();
// console.log(privateKey); // ReferenceError: privateKey is not defined
```

---

### Q4: `this` Keyword, Function Borrowing & Explicit Binding (`call`, `apply`, `bind`) ⭐⭐⭐
**Question:** How is `this` determined in JavaScript? What is function borrowing? Compare `call()`, `apply()`, and `bind()`.

**Answer:**
In JavaScript, `this` is determined by **how a function is invoked** (Runtime binding), except for arrow functions (Lexical binding).

#### 4 Rules of `this`:
1. **Default Binding**: Global `window` (or `undefined` in strict mode `'use strict'`).
2. **Implicit Binding**: Object before the dot (`user.getProfile()` $ightarrow$ `this` is `user`).
3. **Explicit Binding**: `call()`, `apply()`, `bind()`.
4. **`new` Binding**: New instance object created by constructor.
5. **Arrow Functions**: Do not have their own `this`; capture `this` lexically from parent.

#### Function Borrowing with `call`, `apply`, `bind`:
```javascript
const developer = {
  name: "Utkarsh",
  introduce: function(greeting, role) {
    return `${greeting}, I am ${this.name}, a ${role}.`;
  }
};

const designer = { name: "Sarah" };

// Borrowing using call (comma-separated args):
console.log(developer.introduce.call(designer, "Hello", "UI/UX Designer"));

// Borrowing using apply (arguments array):
console.log(developer.introduce.apply(designer, ["Hi", "Product Designer"]));

// Borrowing using bind (returns new bound function):
const boundIntro = developer.introduce.bind(designer, "Hey");
console.log(boundIntro("Lead Designer"));
```

---

### Q5: Currying vs Partial Application
**Question:** What is the difference between Currying and Partial Application?

**Answer:**
- **Currying**: Transforms a function of $N$ arguments into $N$ chained functions, each taking **exactly 1 argument** (`f(a, b, c)` $ightarrow$ `f(a)(b)(c)`).
- **Partial Application**: Fixes a few arguments of a function producing a new function of **lower arity** (`f(a, b, c)` $ightarrow$ `f(a)(b, c)`).

```javascript
// Currying:
const curryAdd = a => b => c => a + b + c;
console.log(curryAdd(1)(2)(3)); // 6

// Partial Application:
function multiply(a, b, c) { return a * b * c; }
const partialMultiplyBy2 = multiply.bind(null, 2);
console.log(partialMultiplyBy2(3, 4)); // 24 (2 * 3 * 4)
```

---

### Q6: Shallow Copy vs Deep Copy & Deep Clone Techniques
**Question:** How does Shallow Copy differ from Deep Copy? Compare `structuredClone`, `JSON.parse(JSON.stringify())`, and custom recursive cloning.

**Answer:**
- **Shallow Copy**: Duplicates the top level; nested objects share the same memory reference (`{ ...obj }`, `Object.assign()`).
- **Deep Copy**: Clones all nested levels recursively into independent memory allocations.

```javascript
const original = {
  name: "Utkarsh",
  skills: ["React", "Node"],
  date: new Date(),
  map: new Map([["key", "value"]])
};

// 1. structuredClone (Modern Standard):
const deep1 = structuredClone(original);

// 2. JSON serialization (Limitations: drops functions, undefined, symbols, converts Date to string, breaks on circular references):
const deep2 = JSON.parse(JSON.stringify(original));
```

---

### Q7: Common Data Transformations: Grouping, Flattening & Deduplicating
**Question:** How do you group objects by property, flatten nested arrays, and remove duplicates from an array of objects in modern JavaScript?

**Answer:**

```javascript
// 1. Group by Property (Object.groupBy in ES2024 or reduce)
const employees = [
  { name: "Alice", dept: "Engineering" },
  { name: "Bob", dept: "HR" },
  { name: "Charlie", dept: "Engineering" }
];
const grouped = employees.reduce((acc, emp) => {
  acc[emp.dept] = acc[emp.dept] || [];
  acc[emp.dept].push(emp);
  return acc;
}, {});

// 2. Flatten Nested Array (arr.flat(Infinity))
const nested = [1, [2, [3, [4, 5]]]];
console.log(nested.flat(Infinity)); // [1, 2, 3, 4, 5]

// 3. Remove Duplicate Objects by ID:
const users = [
  { id: 1, name: "Utkarsh" },
  { id: 2, name: "Alex" },
  { id: 1, name: "Utkarsh" }
];
const uniqueUsers = Array.from(new Map(users.map(u => [u.id, u])).values());
console.log(uniqueUsers); // [{id: 1, name: "Utkarsh"}, {id: 2, name: "Alex"}]
```

---

### Q8: Sequential vs Concurrent Promise Execution
**Question:** How do you execute an array of async tasks sequentially vs concurrently?

**Answer:**

```javascript
const task = (id, ms) => () => new Promise(res => setTimeout(() => {
  console.log(`Task ${id} completed`);
  res(id);
}, ms));

const tasks = [task(1, 300), task(2, 200), task(3, 100)];

// 1. Concurrent Execution (Runs in parallel, takes max(300, 200, 100) = 300ms):
async function runConcurrent() {
  const results = await Promise.all(tasks.map(t => t()));
  console.log("All concurrent finished:", results);
}

// 2. Sequential Execution (Runs one after another, takes 300 + 200 + 100 = 600ms):
async function runSequential() {
  const results = [];
  for (const t of tasks) {
    results.push(await t());
  }
  console.log("All sequential finished:", results);
}
```
