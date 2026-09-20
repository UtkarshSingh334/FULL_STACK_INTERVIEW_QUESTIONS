# ⚛️ React - Medium Questions From Notes

> **Topics from Notes Covered:** `useRef`, Context API, Rendering Website Optimization (`React.memo`, `useMemo`, `useCallback`), CORS handling in frontend/full-stack.

---

### Q1: `useRef`
**Question (From Notes):** What is `useRef` and what are its primary use cases?

**Answer:**
`useRef(initialValue)` returns a mutable object `{ current: initialValue }` whose reference persists across renders.
- **Key Property**: Modifying `.current` **does NOT trigger a component re-render**.

**Use Cases:**
1. **Direct DOM Access**: Focusing inputs, measuring element sizes, canvas drawing.
2. **Storing Mutable Values Across Renders**: Storing interval/timeout IDs, previous state values.

```jsx
import React, { useState, useRef } from 'react';

export function TimerApp() {
  const [seconds, setSeconds] = useState(0);
  const timerRef = useRef(null); // Holds timer ID without re-rendering
  const inputRef = useRef(null); // Direct DOM node

  const start = () => {
    if (timerRef.current) return;
    timerRef.current = setInterval(() => setSeconds(s => s + 1), 1000);
  };

  const stop = () => {
    clearInterval(timerRef.current);
    timerRef.current = null;
  };

  return (
    <div>
      <input ref={inputRef} placeholder="Focus me..." />
      <button onClick={() => inputRef.current.focus()}>Focus</button>
      <h2>Seconds: {seconds}</h2>
      <button onClick={start}>Start</button>
      <button onClick={stop}>Stop</button>
    </div>
  );
}
```

---

### Q2: Context API
**Question (From Notes):** What is the React Context API and what problem does it solve?

**Answer:**
Context API provides a way to pass data through the component tree without having to pass props down manually at every level (**Props Drilling**).

```jsx
import React, { createContext, useContext, useState } from 'react';

const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [theme, setTheme] = useState("dark");
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export function ThemedButton() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button onClick={() => setTheme(theme === "dark" ? "light" : "dark")}>
      Current: {theme}
    </button>
  );
}
```

---

### Q3: Rendering Website: How We Make Website More Optimized
**Question (From Notes):** How do we optimize React website rendering performance?

**Answer:**
1. **`React.memo`**: Skips re-rendering a component if its props haven't changed (shallow comparison).
2. **`useMemo`**: Caches the result of an expensive calculation.
3. **`useCallback`**: Caches function instances so child components receiving functions as props don't re-render unnecessarily.
4. **Code Splitting (`React.lazy` & `Suspense`)**: Loads routes/components on-demand to reduce initial bundle size.

```jsx
import React, { useState, useMemo, useCallback } from 'react';

const UserItem = React.memo(({ user, onDelete }) => {
  return (
    <div>
      <span>{user.name}</span>
      <button onClick={() => onDelete(user.id)}>Delete</button>
    </div>
  );
});

export function UserList({ users }) {
  const [query, setQuery] = useState("");

  const filtered = useMemo(() => {
    return users.filter(u => u.name.toLowerCase().includes(query.toLowerCase()));
  }, [users, query]);

  const handleDelete = useCallback((id) => {
    console.log("Delete user:", id);
  }, []);

  return (
    <div>
      <input value={query} onChange={e => setQuery(e.target.value)} />
      {filtered.map(u => (
        <UserItem key={u.id} user={u} onDelete={handleDelete} />
      ))}
    </div>
  );
}
```

---

### Q4: CORS (Cross-Origin Resource Sharing)
**Question (From Notes):** What is CORS, and why do frontend applications run into CORS errors?

**Answer:**
CORS is a browser security mechanism that restricts a web application on one domain (e.g. `http://localhost:3000`) from requesting resources from a different domain (e.g. `http://api.backend.com`) unless the backend sends the appropriate HTTP response header:
`Access-Control-Allow-Origin: http://localhost:3000`
