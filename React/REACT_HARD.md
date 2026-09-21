# ⚛️ React - Advanced / Hard Questions

> **Topics Covered:** React Fiber Architecture (Reconciliation vs Commit Phases, Priority Lanes), React 18+ Concurrency (`useTransition`, `useDeferredValue`, Suspense), Code Splitting & Lazy Loading (`React.lazy`), Error Boundaries, Performance Profiling & Windowing / Virtualization.

---

### Q1: React Fiber Architecture Deep Dive ⭐⭐⭐
**Question:** What is React Fiber? How does it differ from the legacy Stack Reconciler? Explain Priority Lanes and the 2-phase rendering cycle.

**Answer:**
- **React 15 Stack Reconciler**: Synchronous and recursive. Once rendering started, it could not be paused or interrupted, causing dropped frames (jank) during heavy UI rendering.
- **React 16+ Fiber Reconciler**: Complete rewrite of React's core algorithm. Fiber represents a unit of work as a linked list of virtual fiber nodes.
- **Key Features of Fiber:**
  1. **Pause, Resume, and Abort Work**: Work can be split into chunks across browser frames (`requestIdleCallback` / scheduler).
  2. **Priority Lanes**: High-priority user interactions (typing, clicking) interrupt low-priority offscreen rendering.
  3. **Two-Phase Architecture**:
     - **Phase 1: Render Phase (Asynchronous)**: React traverses fiber tree, calls component functions, calculates diffs. Can be paused, restarted, or aborted without side effects.
     - **Phase 2: Commit Phase (Synchronous)**: React applies all DOM mutations, updates refs, and runs layout effects. Cannot be interrupted.

---

### Q2: React 18 Concurrency: `useTransition` vs `useDeferredValue`
**Question:** How does `useTransition()` improve user input responsiveness during heavy re-renders?

**Answer:**
- `useTransition()` lets you mark state updates as **non-urgent transitions**, allowing high-priority updates (e.g. typing in an input) to execute immediately without being blocked by heavy list filtering.

```jsx
import { useState, useTransition } from 'react';

function SearchComponent({ bigList }) {
  const [input, setInput] = useState('');
  const [list, setList] = useState(bigList);
  const [isPending, startTransition] = useTransition();

  const handleChange = (e) => {
    // 1. Urgent: Immediate typing feedback
    setInput(e.target.value);

    // 2. Non-Urgent: Heavy list filtering deferred
    startTransition(() => {
      setList(bigList.filter(item => item.includes(e.target.value)));
    });
  };

  return (
    <div>
      <input value={input} onChange={handleChange} />
      {isPending && <p>Filtering list...</p>}
      <ItemList items={list} />
    </div>
  );
}
```

---

### Q3: Error Boundaries in React
**Question:** What are Error Boundaries? How do you implement them and what errors do they NOT catch?

**Answer:**
- **Error Boundaries** are React components that catch JavaScript errors anywhere in their child component tree, log the errors, and display a fallback UI instead of crashing the whole app.
- Must be implemented as **Class Components** using `getDerivedStateFromError` (renders fallback) and `componentDidCatch` (logs error).

```jsx
import React from 'react';

class ErrorBoundary extends React.Component {
  constructor(props) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError(error) {
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    console.error("Uncaught error:", error, errorInfo);
  }

  returnFallback() {
    return <h2>Something went wrong. Please refresh.</h2>;
  }

  render() {
    if (this.state.hasError) {
      return this.props.fallback || this.returnFallback();
    }
    return this.props.children;
  }
}
```

**Errors NOT Caught by Error Boundaries:**
1. Event handlers (`onClick` - use standard `try/catch` inside handlers).
2. Asynchronous code (`setTimeout`, `requestAnimationFrame`).
3. Server-Side Rendering (SSR).
4. Errors thrown inside the Error Boundary component itself.
