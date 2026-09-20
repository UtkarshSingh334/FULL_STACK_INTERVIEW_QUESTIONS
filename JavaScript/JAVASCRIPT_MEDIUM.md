# 📜 JavaScript - Medium Questions From Notes

> **Topics from Notes Covered:** Shallow Copy vs Deep Copy, `call`/`apply`/`bind`, `map` vs `filter` vs `reduce`, Scope Chaining & Lexical Scope, Currying, Debouncing vs Throttling, Reference Error (Error types), Prototype (OOP), All Promises (Pending, Fulfilled, Rejected, Async/Await, Callback Hell), Event Delegation (`e.bubble`, Event Propagation, Capturing Phase), Flatten Array.

---

### Q1: Shallow Copy vs Deep Copy
**Question (From Notes):** What is the difference between Shallow Copy and Deep Copy? How do you implement them?

**Answer:**
- **Shallow Copy**: Copies only top-level properties. Nested objects/arrays remain shared references in memory.
- **Deep Copy**: Recursively duplicates all nested objects and arrays into brand new memory allocations.

```javascript
const user = { name: "Utkarsh", skills: ["React", "Node"] };

// Shallow Copy (Spread)
const shallow = { ...user };
shallow.skills.push("MongoDB");
console.log(user.skills); // ['React', 'Node', 'MongoDB'] -> Mutated!

// Deep Copy (structuredClone)
const deep = structuredClone(user);
deep.skills.push("GraphQL");
console.log(user.skills); // ['React', 'Node', 'MongoDB'] -> Unchanged!
```

---

### Q2: `call()`, `apply()`, and `bind()`
**Question (From Notes):** Explain `call`, `apply`, and `bind` with examples.

**Answer:**
- `call(thisArg, arg1, arg2)`: Executes function immediately with specified `this` and comma-separated arguments.
- `apply(thisArg, [arg1, arg2])`: Executes function immediately with arguments passed as an array.
- `bind(thisArg, ...args)`: Returns a **new function** permanently bound to `thisArg`.

```javascript
const person = {
  fullName: function(city) {
    return `${this.firstName} ${this.lastName} from ${city}`;
  }
};
const user = { firstName: "Utkarsh", lastName: "Singh" };

console.log(person.fullName.call(user, "Bangalore"));
console.log(person.fullName.apply(user, ["Bangalore"]));

const boundFn = person.fullName.bind(user, "Bangalore");
console.log(boundFn());
```

---

### Q3: `map()` vs `filter()` vs `reduce()` Function
**Question (From Notes):** Compare `map`, `filter`, and `reduce` functions in JavaScript.

**Answer:**
- `map(cb)`: Transforms each element and returns a new array of the **same length**.
- `filter(cb)`: Returns a new array containing only elements that satisfy the truthy condition.
- `reduce(cb, initialValue)`: Accumulates array elements into a **single value** (object, number, array).

```javascript
const numbers = [1, 2, 3, 4, 5];

const doubled = numbers.map(n => n * 2);        // [2, 4, 6, 8, 10]
const evens = numbers.filter(n => n % 2 === 0);  // [2, 4]
const sum = numbers.reduce((acc, curr) => acc + curr, 0); // 15
```

---

### Q4: Scope, Scope Chaining & Lexical Scope
**Question (From Notes):** Explain Scope, Scope Chaining, and Lexical Scope.

**Answer:**
- **Lexical Scope**: Scope is determined at write/compile time by where variables and blocks are authored.
- **Scope Chain**: When resolving a variable, JS searches Local Scope $\rightarrow$ Outer Enclosing Function Scopes $\rightarrow$ Global Scope. If not found anywhere, it throws a `ReferenceError`.
- **Closure**: Inner function retaining access to outer lexical scope even after the outer function has returned.

```javascript
function outer() {
  const outerVar = "I am outer";
  function inner() {
    console.log(outerVar); // Accesses outerVar via scope chain
  }
  return inner;
}
const fn = outer();
fn(); // "I am outer"
```

---

### Q5: Currying
**Question (From Notes):** What is Currying? Implement infinite currying `sum(1)(2)(3)...()`.

**Answer:**
Currying transforms a multi-argument function $f(a, b, c)$ into a sequence of unary functions $f(a)(b)(c)$.

```javascript
function sum(a) {
  return function(b) {
    if (b !== undefined) {
      return sum(a + b);
    }
    return a;
  };
}

console.log(sum(1)(2)(3)(4)()); // 10
```

---

### Q6: Event Propagation: Event Bubbling (`e.bubble`), Capturing Phase & Event Delegation
**Question (From Notes):** Explain Event Bubbling, Capturing, and Event Delegation.

**Answer:**
1. **Capturing Phase**: Event travels down from `window` $\rightarrow$ Target element.
2. **Target Phase**: Event arrives at clicked target.
3. **Bubbling Phase**: Event bubbles upward from Target $\rightarrow$ `window`.

**Event Delegation**: Attach one event listener to a parent container to handle events on dynamic child elements via event bubbling.

```javascript
document.getElementById("todo-list").addEventListener("click", (e) => {
  if (e.target.matches("button.delete-btn")) {
    e.target.closest("li").remove();
  }
});
```

---

### Q7: Debouncing vs Throttling
**Question (From Notes):** Differentiate Debouncing vs Throttling with implementations.

**Answer:**
- **Debouncing**: Delays execution until a specified quiet period with no new calls has elapsed (Search input).
- **Throttling**: Executes at most once per specified time interval (Scroll / Resize handlers).

```javascript
// Debounce
function debounce(fn, delay) {
  let timer;
  return function(...args) {
    clearTimeout(timer);
    timer = setTimeout(() => fn.apply(this, args), delay);
  };
}

// Throttle
function throttle(fn, limit) {
  let inThrottle = false;
  return function(...args) {
    if (!inThrottle) {
      fn.apply(this, args);
      inThrottle = true;
      setTimeout(() => inThrottle = false, limit);
    }
  };
}
```

---

### Q8: Reference Error & Common JS Error Types
**Question (From Notes):** What causes a Reference Error in JavaScript?

**Answer:**
1. **`ReferenceError`**: Trying to access a variable that has not been declared, or accessing `let`/`const` inside TDZ.
   ```javascript
   console.log(unassignedVar); // ReferenceError: unassignedVar is not defined
   ```
2. **`TypeError`**: Performing an operation on an incompatible type (e.g., `const x = 1; x = 2;` or `null.toString()`).
3. **`SyntaxError`**: Code violating language syntax.

---

### Q9: Prototype (OOP & Prototypal Inheritance)
**Question (From Notes):** Explain Prototype in JavaScript OOP.

**Answer:**
JavaScript objects inherit properties and methods directly from other objects via the **Prototype Chain**.

```javascript
function Animal(name) {
  this.name = name;
}
Animal.prototype.speak = function() {
  return `${this.name} makes a sound.`;
};

function Dog(name) {
  Animal.call(this, name);
}
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

const d = new Dog("Buddy");
console.log(d.speak()); // "Buddy makes a sound." (Traversed prototype chain)
```

---

### Q10: All Promises (Pending, Fulfilled, Rejected), Async/Await & Callback Hell
**Question (From Notes):** Explain Promise states (Pending, Fulfilled, Rejected), Callback Hell, and Async/Await.

**Answer:**
- **Promise States**:
  1. `Pending`: Initial state, neither fulfilled nor rejected.
  2. `Fulfilled`: Operation completed successfully (`resolve()`).
  3. `Rejected`: Operation failed (`reject()`).
- **Callback Hell**: Deeply nested callbacks forming a "Pyramid of Doom", making code unreadable and error handling difficult.
- **Async/Await**: Syntactic sugar over Promises enabling synchronous-looking asynchronous code.

```javascript
// Callback Hell
getUser(1, (user) => {
  getOrders(user.id, (orders) => {
    getOrderDetails(orders[0].id, (details) => {
      console.log(details);
    });
  });
});

// Clean Async/Await Solution
async function fetchDetails() {
  try {
    const user = await getUser(1);
    const orders = await getOrders(user.id);
    const details = await getOrderDetails(orders[0].id);
    console.log(details);
  } catch (err) {
    console.error(err);
  }
}
```

---

### Q11: Flatten Array
**Question (From Notes):** Flatten a nested array with arbitrary nesting depth.

```javascript
function flattenArray(arr, depth = 1) {
  if (depth <= 0) return arr.slice();
  return arr.reduce((acc, curr) => {
    if (Array.isArray(curr)) {
      acc.push(...flattenArray(curr, depth - 1));
    } else {
      acc.push(curr);
    }
    return acc;
  }, []);
}

console.log(flattenArray([1, [2, [3, [4, 5]]], 6], Infinity)); // [1, 2, 3, 4, 5, 6]
```
