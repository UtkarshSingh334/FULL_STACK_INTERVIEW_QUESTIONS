# ⚛️ React - Hooks & State Management

> **Topics Covered:** `useState` Internals & Batching, `useEffect` Dependency Array Rules & Cleanups, `useRef` vs `useState`, `useMemo` vs `useCallback` (When NOT to use `useMemo`), `useReducer` vs `useState`, Custom Hooks, Rules of Hooks (Why no loops/conditionals), Context API Flow Structure, Redux Architecture, Redux Toolkit (RTK) `createSlice`, `createAsyncThunk`, RTK Query vs Axios, Redux vs Context API.

---

### Q1: `useState` Internals: Why Direct Mutation Fails & Why React Batches State
**Question:** Why should you never mutate state directly (`state.count++`)? Why and how does React batch state updates?

**Answer:**
1. **Immutability & Reference Equality**: React compares previous and next state using shallow reference equality (`Object.is(prevState, nextState)`). Mutating an object directly keeps the same memory reference pointer, so React believes nothing changed and **skips the re-render**.
2. **Automatic State Batching**: React groups multiple state updates inside event handlers, promises, and `setTimeout` into a single re-render to prevent unnecessary DOM thrashing and maximize frame rates.

```jsx
function Counter() {
  const [count, setCount] = useState(0);

  const handleClick = () => {
    // Batched into 1 render:
    setCount(c => c + 1);
    setCount(c => c + 1);
    setCount(c => c + 1); // count safely becomes 3
  };

  return <button onClick={handleClick}>{count}</button>;
}
```

---

### Q2: `useEffect` Dependency Array In-Depth & Cleanup Functions
**Question:** Explain what happens when the dependency array in `useEffect` is empty, omitted, or contains values. What is the cleanup function for?

**Answer:**
- **No Array (`useEffect(fn)`)**: Runs on initial mount and **after every single render**.
- **Empty Array (`useEffect(fn, [])`)**: Runs **only once after initial mount** (`componentDidMount`).
- **With Dependencies (`useEffect(fn, [a, b])`)**: Runs on mount and whenever `a` or `b` reference changes.
- **Cleanup Function**:
  - Returned from the effect function.
  - Runs before the component unmounts AND before re-running the effect on dependency change.
  - Used to **unsubscribe from WebSockets, clear `setInterval` timers, and abort ongoing `fetch` requests** (`AbortController`).

```jsx
useEffect(() => {
  const controller = new AbortController();

  fetch(`/api/data`, { signal: controller.signal })
    .then(res => res.json())
    .then(setData)
    .catch(err => { if (err.name !== 'AbortError') console.error(err); });

  return () => controller.abort(); // Cleanup cancels pending network request on unmount
}, [query]);
```

---

### Q3: `useRef()` vs `useState()`
**Question:** Compare `useRef` and `useState`. When should each be used?

**Answer:**
| Feature | `useState` | `useRef` |
| :--- | :--- | :--- |
| **Return Value** | `[state, setState]` | `{ current: initialValue }` object |
| **Causes Re-render?**| ✅ Yes, calling updater triggers re-render | ❌ No, mutating `.current` never triggers re-render |
| **Memory Persistence**| Persists state across renders | Persists reference across renders |
| **Primary Use Cases** | Dynamic UI values that must update screen | Direct DOM access, storing timer IDs, previous values |

---

### Q4: `useMemo()` vs `useCallback()` & When NOT to Use `useMemo`
**Question:** Differentiate between `useMemo` and `useCallback`. When is `useMemo` harmful to performance?

**Answer:**
- **`useMemo(() => computeValue(a), [a])`**: Caches and returns the **result value** of an expensive calculation.
- **`useCallback(fn, [deps])`**: Caches and returns the **function reference definition itself** to prevent re-creating functions on every render.
- **When NOT to use `useMemo`**:
  - For cheap/trivial operations (e.g. `2 + 2` or filtering small 10-item arrays). The overhead of creating a closure, checking dependency arrays, and maintaining cache memory costs MORE CPU than simply recalculating.

---

### Q5: `useReducer()` vs `useState()`: When to Switch?
**Question:** What is `useReducer` and when should you choose it over `useState`?

**Answer:**
- Choose **`useState`** for independent, simple primitive values (e.g., toggles, modals, single input strings).
- Choose **`useReducer`** when:
  1. State logic involves **complex nested objects or arrays**.
  2. The next state depends on multiple sub-values of the previous state.
  3. Multiple actions can transition state in predictable ways (e.g., checkout flows, complex filter forms).

```jsx
import { useReducer } from 'react';

const initialState = { count: 0, step: 1 };
function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT': return { ...state, count: state.count + state.step };
    case 'SET_STEP': return { ...state, step: action.payload };
    case 'RESET': return initialState;
    default: return state;
  }
}
```

---

### Q6: Rules of Hooks: Why Can't Hooks be Called in Loops or Conditionals?
**Question:** Explain the two Rules of Hooks. Why does React break if a hook is called inside an `if` block or loop?

**Answer:**
1. **Rule 1**: Only call hooks at the top level (Never inside loops, conditions, or nested functions).
2. **Rule 2**: Only call hooks from React function components or custom hooks.
- **Under the Hood Reason**: React tracks hooks for each component as a **singly linked list / array of hook state cells**, relying solely on the **order of hook calls** between renders. If a hook is inside a conditional, the sequence shifts on the next render, causing React to assign the wrong hook state to the wrong variable!

---

### Q7: Redux Toolkit (RTK) vs Traditional Redux & Redux Data Flow ⭐⭐⭐
**Question:** Explain the unidirectional Redux data flow. How does Redux Toolkit (`createSlice`) eliminate boilerplate?

**Answer:**
- **Redux Unidirectional Flow:**
  ```
  User Interaction (UI) --> dispatch(Action) --> Middleware --> Reducer (Pure Function) --> Store Updated --> UI Re-renders via useSelector
  ```
- **Redux Toolkit (`createSlice`) Innovations:**
  1. Automatically generates action creators and action types from reducer keys.
  2. Integrates **Immer** library internally, allowing developers to write direct "mutations" (`state.value++`) which safely produce immutable updates under the hood.
  3. Pre-configures Redux DevTools and `redux-thunk` middleware automatically via `configureStore()`.

```javascript
import { createSlice, configureStore } from '@reduxjs/toolkit';

const counterSlice = createSlice({
  name: 'counter',
  initialState: { value: 0 },
  reducers: {
    increment: (state) => { state.value += 1; }, // Immer handles immutability!
    decrement: (state) => { state.value -= 1; },
  },
});

export const { increment, decrement } = counterSlice.actions;
export const store = configureStore({ reducer: { counter: counterSlice.reducer } });
```

---

### Q8: RTK Query vs Axios & Redux vs Context API
**Question:** Compare RTK Query with Axios, and Redux with Context API. When should you NOT use Redux?

**Answer:**
- **RTK Query vs Axios**:
  - *Axios*: Raw HTTP client. Requires manual boilerplate for tracking `isLoading`, `isError`, state caching, and de-duplication.
  - *RTK Query*: Complete server-state caching solution. Automatically eliminates duplicate requests, caches responses, provides polling, optimistic updates, and manages loading/error states out of the box.
- **Redux vs Context API**:
  - *Context API*: Low-frequency, static global state (Themes, Auth User profile, Language). Every consumer re-renders on context value update unless carefully memoized.
  - *Redux*: High-frequency, complex state across large decoupled applications with time-travel debugging.
- **When NOT to use Redux**: Small/medium apps, local form states, or when React Query / RTK Query already handles server state.
