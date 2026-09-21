# ⚛️ React - Medium Questions

> **Topics Covered:** `useEffect` Lifecycle & Cleanup, `useRef` (DOM Access & Mutable Values), Context API Flow Structure (In-Depth), `useReducer` Hook & State Management (In-Depth), `useReducer` vs Redux vs RTK vs RTK Query (In-Depth Architecture Matrix), `useMemo` vs `useCallback`, Controlled vs Uncontrolled Components, Custom Hooks.

---

### Q1: `useEffect` Hook Lifecycle & Cleanup ⭐⭐
**Question:** Explain the dependency array in `useEffect`. How do you replicate `componentDidMount`, `componentDidUpdate`, and `componentWillUnmount`?

**Answer:**
- **No Dependency Array**: Runs on initial mount and **after every single re-render**.
- **Empty Array (`[]`)**: Runs **only once on mount** (`componentDidMount`).
- **With Dependencies (`[a, b]`)**: Runs on mount and whenever `a` or `b` value changes (`componentDidUpdate`).
- **Cleanup Function**: Returned by the effect; runs before the component unmounts (`componentWillUnmount`) and before re-running the effect on dependency change (cancels active timers, removes event listeners, aborts network fetch).

```jsx
import { useEffect, useState } from 'react';

function WindowTracker() {
  const [width, setWidth] = useState(window.innerWidth);

  useEffect(() => {
    const handleResize = () => setWidth(window.innerWidth);
    window.addEventListener('resize', handleResize);

    // Cleanup function
    return () => {
      window.removeEventListener('resize', handleResize);
    };
  }, []); // Empty array: Setup once on mount, cleanup on unmount

  return <p>Window Width: {width}px</p>;
}
```

---

### Q2: `useRef` Hook: DOM References & Mutable Values
**Question:** What is `useRef` and how does it differ from `useState`?

**Answer:**
- **`useRef(initialValue)`** returns a mutable ref object `{ current: initialValue }` whose `.current` property persists for the entire lifetime of the component.
- **Key Difference:** Updating `ref.current` **does not trigger a component re-render**, whereas updating `useState` always triggers a re-render.

#### Two Primary Use Cases:
1. **Accessing underlying Real DOM nodes** (Focus input, measure element dimensions, scroll to view).
2. **Storing mutable instance variables** without re-rendering (Timer IDs, previous prop values).

```jsx
import { useRef, useEffect } from 'react';

function AutoFocusInput() {
  const inputRef = useRef(null);
  const renderCount = useRef(1);

  useEffect(() => {
    inputRef.current.focus(); // Direct DOM access
  }, []);

  useEffect(() => {
    renderCount.current += 1; // Tracks renders without causing infinite loop
  });

  return <input ref={inputRef} placeholder="Focused on load" />;
}
```

---

### Q3: Context API Flow Structure ⭐⭐⭐
**Question:** Explain the React Context API flow structure. How does it prevent Prop Drilling? Provide a complete implementation example with separate context and provider files.

**Answer:**
- **Prop Drilling Problem**: Passing props down through multiple intermediary component layers that do not need the data themselves just to reach a deeply nested child.
- **Context API Flow:**
  ```
  1. createContext() --> Creates Context Object
  2. <Context.Provider value={...}> --> Wraps Component Tree & Supplies Global Value
  3. useContext(Context) --> Deeply nested components consume value directly
  ```

#### Recommended Architecture: Separate Provider Pattern

```jsx
// 1. context/AuthContext.jsx
import { createContext, useContext, useState } from 'react';

const AuthContext = createContext(null);

export function AuthProvider({ children }) {
  const [user, setUser] = useState(null);

  const login = (userData) => setUser(userData);
  const logout = () => setUser(null);

  return (
    <AuthContext.Provider value={{ user, login, logout, isAuthenticated: !!user }}>
      {children}
    </AuthContext.Provider>
  );
}

// Custom Hook for clean consumption
export function useAuth() {
  const context = useContext(AuthContext);
  if (!context) {
    throw new Error('useAuth must be used within an AuthProvider');
  }
  return context;
}
```

```jsx
// 2. main.jsx - Wrap Application
import { AuthProvider } from './context/AuthContext';
import App from './App';

ReactDOM.createRoot(document.getElementById('root')).render(
  <AuthProvider>
    <App />
  </AuthProvider>
);
```

```jsx
// 3. components/Navbar.jsx - Direct Consumption
import { useAuth } from '../context/AuthContext';

export function Navbar() {
  const { user, logout, isAuthenticated } = useAuth();

  return (
    <nav>
      {isAuthenticated ? (
        <div>
          <span>Welcome, {user.name}</span>
          <button onClick={logout}>Logout</button>
        </div>
      ) : (
        <span>Please Log In</span>
      )}
    </nav>
  );
}
```

---

### Q4: `useReducer()` Hook: Managing Complex State ⭐⭐⭐
**Question:** What is `useReducer()`? Explain its flow, syntax, action payloads, and pure reducer rules. Compare `useState()` vs `useReducer()`.

**Answer:**
`useReducer()` is a React Hook designed for **complex state logic** where the next state depends on the previous state or involves multiple sub-values.

#### Syntax & Flow:
```
const [state, dispatch] = useReducer(reducer, initialState);
UI Event --> dispatch({ type: 'ACTION_TYPE', payload: data }) --> Reducer(state, action) --> New State --> Re-render
```

#### Rules of a Reducer Function:
1. **Must be a Pure Function**: No side effects (no API calls, timers, or random numbers inside reducer).
2. **Never Mutate State**: Always return a new state object using spread `{ ...state, key: value }`.

#### Complete Form Example:
```jsx
import { useReducer } from 'react';

const initialState = { name: '', email: '', count: 0 };

function formReducer(state, action) {
  switch (action.type) {
    case 'SET_FIELD':
      return { ...state, [action.field]: action.payload };
    case 'INCREMENT_COUNT':
      return { ...state, count: state.count + 1 };
    case 'RESET':
      return initialState;
    default:
      throw new Error(`Unhandled action type: ${action.type}`);
  }
}

export function RegistrationForm() {
  const [state, dispatch] = useReducer(formReducer, initialState);

  return (
    <form onSubmit={(e) => e.preventDefault()}>
      <input 
        value={state.name} 
        onChange={(e) => dispatch({ type: 'SET_FIELD', field: 'name', payload: e.target.value })} 
        placeholder="Name" 
      />
      <input 
        value={state.email} 
        onChange={(e) => dispatch({ type: 'SET_FIELD', field: 'email', payload: e.target.value })} 
        placeholder="Email" 
      />
      <p>Click Count: {state.count}</p>
      <button type="button" onClick={() => dispatch({ type: 'INCREMENT_COUNT' })}>Increment</button>
      <button type="button" onClick={() => dispatch({ type: 'RESET' })}>Reset</button>
    </form>
  );
}
```

---

### Q5: `useReducer` vs Redux vs Redux Toolkit (RTK) vs RTK Query ⭐⭐⭐
**Question:** Compare `useReducer`, Redux, Redux Toolkit (RTK), and RTK Query in terms of architecture, boilerplate, caching, and use cases.

**Answer:**

| Feature | `useReducer()` | Traditional Redux | Redux Toolkit (RTK) | RTK Query |
| :--- | :--- | :--- | :--- | :--- |
| **Scope** | Local component / context tree | Global application store | Global application store | Global Server State & Caching |
| **Boilerplate** | Low | High (Action creators, constants, reducers) | Low (`createSlice` bundles actions + reducers) | Extremely Low (Declarative API slices) |
| **State Mutation** | Manual immutable copies (`{...state}`) | Manual immutable copies | Uses **Immer** internally (write "mutating" logic safely) | Automatic normalized caching |
| **Async Handling** | Requires manual `useEffect` / callbacks | Requires `redux-thunk` / `redux-saga` | Built-in `createAsyncThunk` | Built-in (Automatic `isLoading`, `isError`, refetching) |
| **Best For** | Medium local complex state | Legacy codebases | Global client UI state | Backend API data fetching, mutations, and caching |

#### Modern Redux Toolkit (RTK) + RTK Query Example:

```javascript
// 1. store/apiSlice.js (RTK Query)
import { createApi, fetchBaseQuery } from '@reduxjs/toolkit/query/react';

export const userApi = createApi({
  reducerPath: 'userApi',
  baseQuery: fetchBaseQuery({ baseUrl: 'https://api.example.com/' }),
  tagTypes: ['User'],
  endpoints: (builder) => ({
    getUsers: builder.query({
      query: () => 'users',
      providesTags: ['User'],
    }),
    addUser: builder.mutation({
      query: (newUser) => ({
        url: 'users',
        method: 'POST',
        body: newUser,
      }),
      invalidatesTags: ['User'], // Auto-refetches getUsers on mutation!
    }),
  }),
});

export const { useGetUsersQuery, useAddUserMutation } = userApi;
```

```javascript
// 2. store/store.js
import { configureStore } from '@reduxjs/toolkit';
import { userApi } from './apiSlice';

export const store = configureStore({
  reducer: {
    [userApi.reducerPath]: userApi.reducer,
  },
  middleware: (getDefaultMiddleware) =>
    getDefaultMiddleware().concat(userApi.middleware),
});
```

```jsx
// 3. components/UserList.jsx
import { useGetUsersQuery } from '../store/apiSlice';

export function UserList() {
  const { data: users, isLoading, isError } = useGetUsersQuery();

  if (isLoading) return <p>Loading users...</p>;
  if (isError) return <p>Error loading data.</p>;

  return (
    <ul>
      {users.map(u => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
}
```

---

### Q6: `useMemo` vs `useCallback`
**Question:** What is the difference between `useMemo` and `useCallback`? When should you use them?

**Answer:**
- **`useMemo(() => fn(), [deps])`**: Caches and returns the **computed return value** of an expensive calculation to avoid recalculating on every re-render.
- **`useCallback(fn, [deps])`**: Caches and returns the **function instance definition itself** to prevent child components wrapped in `React.memo` from re-rendering due to new function memory references.

```jsx
import { useState, useMemo, useCallback } from 'react';

function ProductDashboard({ products }) {
  const [query, setQuery] = useState('');

  // useMemo: Memoizes filtered array result
  const filteredProducts = useMemo(() => {
    return products.filter(p => p.name.toLowerCase().includes(query.toLowerCase()));
  }, [products, query]);

  // useCallback: Memoizes function reference passed to memoized child
  const handleDelete = useCallback((id) => {
    console.log("Delete product ID:", id);
  }, []);

  return <ProductList items={filteredProducts} onDelete={handleDelete} />;
}
```

---

### Q7: Controlled vs Uncontrolled Components
**Question:** Compare Controlled vs Uncontrolled components in React.

**Answer:**
- **Controlled Component**: Input form data is handled by React component state (`value={state}` + `onChange={setState}`). Single source of truth.
- **Uncontrolled Component**: Input form data is handled by the browser Real DOM itself; accessed on submit via `useRef`.
