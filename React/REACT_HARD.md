# ⚛️ React - Advanced Architecture & Concurrency

> **Topics Covered:** React Fiber Architecture (Units of Work, Priority Lanes), Concurrent React (`useTransition`, `useDeferredValue`, Suspense for Data Fetching), Code Splitting & Dynamic Imports (`React.lazy`), Error Boundaries & Uncaught Exceptions, React Performance Optimization & Windowing.

---

### Q1: React Fiber Architecture Deep Dive ⭐⭐⭐
**Question:** What is React Fiber? How did it solve the blocking stack reconciler problem?

**Answer:**
- **Old Stack Reconciler (React 15)**: Recursive, synchronous traversal of the component tree. Heavy tree diffing locked the browser main thread, causing frame drops and unresponsive user input.
- **Fiber Reconciler (React 16+)**: Completely re-engineered core algorithm where every Virtual DOM node is modeled as a **Fiber node** in a doubly linked list structure.
- **Core Capabilities of Fiber:**
  1. **Incremental Rendering**: Divides render work into small chunks and yields back to the browser event loop using request scheduling.
  2. **Priority Lanes**: High-priority work (user typing, animations) can interrupt low-priority work (offscreen list rendering).
  3. **2-Phase Rendering Cycle**:
     - *Phase 1 (Render Phase - Asynchronous)*: Traverses fibers, calls component render, calculates diffs. Can be paused, aborted, or restarted without side effects.
     - *Phase 2 (Commit Phase - Synchronous)*: Mutates the Real DOM and runs layout effects. Must finish uninterrupted to avoid partial UI tearing.

---

### Q2: React 18 Concurrency: `useTransition` vs `useDeferredValue`
**Question:** How do `useTransition` and `useDeferredValue` improve user responsiveness during CPU-heavy filtering?

**Answer:**
- **`useTransition()`**: Wraps a state setter to mark it as a non-urgent transition. Returns `[isPending, startTransition]`.
- **`useDeferredValue(val)`**: Defers updating a consumer value until urgent UI updates have finished rendering.

```jsx
import { useState, useTransition, useDeferredValue } from 'react';

function SearchList({ items }) {
  const [query, setQuery] = useState('');
  const [isPending, startTransition] = useTransition();
  const deferredQuery = useDeferredValue(query);

  const handleInput = (e) => {
    // 1. Urgent: Immediate typing response
    setQuery(e.target.value);
  };

  const filtered = items.filter(i => i.name.includes(deferredQuery));

  return (
    <div>
      <input value={query} onChange={handleInput} />
      {isPending && <p>Loading results...</p>}
      <ItemList data={filtered} />
    </div>
  );
}
```
