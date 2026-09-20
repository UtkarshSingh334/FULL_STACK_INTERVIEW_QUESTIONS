# ⚛️ React - Hard Questions From Notes

> **Topics from Notes Covered:** Advanced React Website Optimization, Context API Re-render Mitigation, Custom Hooks Architecture.

---

### Q1: Preventing Context API Re-render Cascades
**Question (From Notes):** How do you optimize React Context API to prevent all consumer components from re-rendering on every state update?

**Answer:**
By default, whenever a Context Provider's value changes, **all** components calling `useContext(MyContext)` re-render, even if they only consume an unchanged property.

**Optimization Strategies:**
1. **Split State and Dispatch Contexts**: Separate mutable state from stable update functions.
2. **Memoize Provider Value**: Always wrap context value in `useMemo`.

```jsx
import React, { createContext, useContext, useReducer, useMemo } from 'react';

const StateContext = createContext();
const DispatchContext = createContext();

function reducer(state, action) {
  switch (action.type) {
    case 'INCREMENT': return { count: state.count + 1 };
    default: return state;
  }
}

export function CounterProvider({ children }) {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <StateContext.Provider value={state}>
      <DispatchContext.Provider value={dispatch}>
        {children}
      </DispatchContext.Provider>
    </StateContext.Provider>
  );
}

// Components only needing dispatch never re-render when state.count changes!
export const useCounterDispatch = () => useContext(DispatchContext);
export const useCounterState = () => useContext(StateContext);
```
