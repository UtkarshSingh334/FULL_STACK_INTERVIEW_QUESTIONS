# ⚛️ React - Easy Questions

> **Topics Covered:** What is React, Virtual DOM & Reconciliation, JSX & Babel Compilation, Functional vs Class Components, Props vs State, One-Way Data Binding, Rules of Hooks, `useState` Hook & Functional State Updates, Lists & Keys (Why index as key is anti-pattern), Conditional Rendering.

---

### Q1: What is React and Why Do We Use It?
**Question:** What is React? What are its primary advantages?

**Answer:**
- **React** is an open-source, component-based JavaScript library for building interactive user interfaces, maintained by Meta.
- **Key Advantages:**
  1. **Component-Based Architecture**: Build encapsulated, reusable UI building blocks.
  2. **Virtual DOM**: Minimizes direct, expensive Real DOM manipulations through efficient batch diffing.
  3. **Declarative UI**: You declare *what* the UI should look like for a given state; React handles rendering.
  4. **Unidirectional (One-Way) Data Flow**: State flows predictably down from parent to child components via props.
  5. **Rich Ecosystem**: Massive community, hooks, SSR frameworks (Next.js), and mobile development (React Native).

---

### Q2: Virtual DOM and Reconciliation ⭐
**Question:** What is the Virtual DOM and how does React update the Real DOM?

**Answer:**
- The **Virtual DOM (VDOM)** is an in-memory lightweight JavaScript representation of the actual Real DOM tree (`React.createElement` objects).
- **The Reconciliation Process (Diffing Algorithm):**
  1. Whenever component state or props change, React creates a new Virtual DOM tree.
  2. **Diffing**: React compares the new VDOM with the previous VDOM snapshot using a fast $O(n)$ heuristic algorithm.
  3. **Batch Update (Commit)**: React calculates the minimum necessary Real DOM mutations (patch) and updates only those specific nodes in the Real DOM.

---

### Q3: What is JSX?
**Question:** What is JSX? Can browsers read JSX directly?

**Answer:**
- **JSX (JavaScript XML)** is a syntax extension for JavaScript that allows you to write HTML-like markup inside JavaScript files.
- **Browsers cannot read JSX directly**: Build tools (like Babel or SWC) compile JSX into standard `React.createElement()` or `_jsx()` function calls before execution.

```jsx
// JSX Code:
const element = <h1 className="title">Hello, React!</h1>;

// Compiled JavaScript (Babel):
const element = React.createElement("h1", { className: "title" }, "Hello, React!");
```

---

### Q4: Functional Components vs Class Components
**Question:** Compare Functional Components and Class Components in React.

**Answer:**
| Feature | Functional Components (Modern) | Class Components (Legacy) |
| :--- | :--- | :--- |
| **Syntax** | Plain JavaScript function | ES6 Class extending `React.Component` |
| **State Management** | React Hooks (`useState`, `useReducer`) | `this.state` and `this.setState()` |
| **Lifecycle** | `useEffect` Hook | `componentDidMount`, `componentDidUpdate`, `componentWillUnmount` |
| **`this` Keyword** | No `this` issues | Requires manual method binding (`this.handleClick.bind(this)`) |
| **Boilerplate** | Lightweight and concise | Verbose boilerplate code |

---

### Q5: Props vs State
**Question:** What is the difference between Props and State?

**Answer:**
| Criteria | Props (Properties) | State |
| :--- | :--- | :--- |
| **Definition** | Data passed into a component from its parent | Internal data managed within the component |
| **Mutability** | **Immutable** (Read-only for child component) | **Mutable** (Updated via `setState` / `useState`) |
| **Ownership** | Owned and controlled by parent component | Owned and private to the local component |
| **Re-render** | Changes in props trigger child re-render | Calling updater function triggers re-render |

---

### Q6: `useState` Hook & Functional State Updates
**Question:** How does `useState` work? Why should you pass a callback function to `setState` when updating based on previous state?

**Answer:**
- `useState` declares a state variable and a setter function.
- **Batching & Stale Closures:** React batches state updates for performance. If you update state multiple times based on the previous value, direct updates will read stale state. Passing an updater function guarantees access to the latest committed state.

```jsx
import { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  const handleTripleIncrement = () => {
    // ❌ Incorrect (Batched: count remains 0 + 1 = 1)
    // setCount(count + 1);
    // setCount(count + 1);
    // setCount(count + 1);

    // ✅ Correct: Functional updates receive the latest pending state
    setCount(prev => prev + 1);
    setCount(prev => prev + 1);
    setCount(prev => prev + 1); // count becomes 3
  };

  return <button onClick={handleTripleIncrement}>Count: {count}</button>;
}
```

---

### Q7: Lists & Keys: Why is Array Index as Key an Anti-Pattern?
**Question:** Why does React require a `key` prop when rendering lists? Why should you avoid using array indices as keys?

**Answer:**
- **Purpose of `key`**: Keys help React identify which items have changed, been added, or been removed during reconciliation.
- **Why array index is dangerous:**
  If the list is re-ordered, filtered, or items are inserted at the beginning/middle, array indices change for existing items. React will wrongly match old component instances to new data, leading to **state corruption in child inputs, animation glitches, and UI bugs**.

```jsx
// ❌ Bad: Index as key
{users.map((user, index) => <UserCard key={index} user={user} />)}

// ✅ Good: Stable, unique identifier as key
{users.map(user => <UserCard key={user.id} user={user} />)}
```

---

### Q8: Rules of Hooks
**Question:** What are the two fundamental Rules of Hooks in React?

**Answer:**
1. **Only Call Hooks at the Top Level**: Do not call hooks inside loops, conditions, or nested functions. This ensures hooks execute in the exact same order on every render.
2. **Only Call Hooks from React Function Components or Custom Hooks**: Never call hooks from standard JavaScript functions or class components.
