# 📜 JavaScript - Advanced & Architecture

> **Topics Covered:** JavaScript Event Loop & Concurrency Model (Call Stack, Web APIs, Microtask vs Macrotask Queue), Promise vs setTimeout Execution Order Puzzle, Prototypes & Prototypal Inheritance, Memory Management & Garbage Collection (Mark-and-Sweep, Memory Leaks), JavaScript `Proxy` and `Reflect` APIs.

---

## 1. The JavaScript Event Loop & Concurrency Architecture

### Answer
JavaScript has a single-threaded runtime (one Call Stack). The **Event Loop** continuously monitors the Call Stack and task queues:
1. **Call Stack**: Executes synchronous code (LIFO).
2. **Microtask Queue (High Priority)**: `Promise.then/catch/finally`, `queueMicrotask()`, `MutationObserver`. Emptied completely after the current stack frame empties.
3. **Macrotask Queue (Standard Priority)**: `setTimeout`, `setInterval`, `setImmediate`, DOM events, I/O. Processed one task per loop iteration.

```
JavaScript Code --> Call Stack --> Web APIs --> Microtask Queue (High Priority) / Macrotask Queue --> Event Loop --> Call Stack
```

---

## 2. Output Puzzle: Promise vs setTimeout Execution Order

### Question: Predict the output and explain why:
```js
console.log("A");

setTimeout(() => {
    console.log("B");
}, 0);

Promise.resolve().then(() => {
    console.log("C");
});

console.log("D");
```

### Answer & Output
```
A
D
C
B
```

### Explanation:
1. Synchronous code executes first: `A` then `D`.
2. `setTimeout` callback goes to **Macrotask Queue**.
3. `Promise.resolve().then` callback goes to **Microtask Queue**.
4. When Call Stack empties, Event Loop processes the **Microtask Queue first** $ightarrow$ prints `C`.
5. Finally, the Event Loop takes the next task from the **Macrotask Queue** $ightarrow$ prints `B`.

---

## 3. Prototypes & Prototypal Inheritance

### Answer
In JavaScript, every object contains an internal link to another object called its **prototype** (`[[Prototype]]` or `__proto__`). When a property is accessed, JavaScript traverses up the **Prototype Chain** until it finds the property or reaches `Object.prototype` (`null`).

### Example
```js
function Person(name) {
    this.name = name;
}
Person.prototype.greet = function() {
    return `Hello, my name is ${this.name}`;
};

const user = new Person("Utkarsh");
console.log(user.greet()); // "Hello, my name is Utkarsh" (Found on Person.prototype)
```

---

## 4. Memory Management & Common Causes of Memory Leaks

### Answer
- **Garbage Collection (Mark-and-Sweep)**: The engine traverses memory starting from "Roots" (global variables, call stack). Objects unreachable from roots are swept and deallocated.
- **Common Memory Leaks:**
  1. **Accidental Global Variables** (`foo = "bar"` without `let/const`).
  2. **Forgotten Timers / Callbacks** (`setInterval` running in background).
  3. **Detached DOM Nodes** (Holding JavaScript references to removed DOM elements).
  4. **Uncleaned Closures** (Holding large arrays in memory indefinitely).

---

## 5. JavaScript `Proxy` and `Reflect` APIs

### Answer
A **`Proxy`** wraps a target object and intercepts fundamental operations (property reading `get`, writing `set`, deletion).

### Example
```js
const state = { count: 0 };

const reactive = new Proxy(state, {
    get(target, prop) {
        console.log(`[Read] Property: ${prop}`);
        return Reflect.get(target, prop);
    },
    set(target, prop, value) {
        console.log(`[Write] ${prop} = ${value}`);
        return Reflect.set(target, prop, value);
    }
});

reactive.count = 10; // Logs write
console.log(reactive.count); // Logs read, returns 10
```
