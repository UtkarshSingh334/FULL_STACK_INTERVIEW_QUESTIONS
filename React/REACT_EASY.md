# ⚛️ React - Easy Questions From Notes

> **Topics from Notes Covered:** States vs Props, State vs Hook, Consoling `useState` (Async batching), `useEffect` (Why `useEffect`, Dependency `[]` Array variations), Lifting State Up (`stateup lifting`), Framework vs Library difference.

---

### Q1: States vs Props
**Question (From Notes):** What is the difference between State and Props in React?

**Answer:**
- **Props (Properties)**: Read-only data passed from parent to child component. Cannot be mutated by the child.
- **State**: Mutable, local data managed internally by a component. Updating state triggers a re-render.

```jsx
// Parent passes props
function Parent() {
  const [theme, setTheme] = useState("dark"); // State
  return <Child currentTheme={theme} />;      // Props
}

// Child receives props
function Child({ currentTheme }) {
  return <div>Current Theme: {currentTheme}</div>;
}
```

---

### Q2: State vs Hook
**Question (From Notes):** What is the difference between State and Hook in React?

**Answer:**
- **State**: The actual dynamic data held in memory by a component.
- **Hook**: A special function (e.g., `useState`, `useEffect`, `useRef`) that lets functional components use React state and lifecycle capabilities without writing class components.

---

### Q3: Consoling `useState` (Why `console.log` shows old state)
**Question (From Notes):** Why does `console.log(state)` print the old state immediately after calling `setState`?

**Answer:**
State updates in React are **asynchronous and batched** for performance. Calling `setCount(count + 1)` schedules an update for the next render; the current execution context retains the old state value from its closure snapshot.

```jsx
const [count, setCount] = useState(0);

const handleClick = () => {
  setCount(count + 1);
  console.log(count); // Prints OLD value (0, not 1)!
};

// Solution 1: Use useEffect to read committed state
useEffect(() => {
  console.log("Updated count on render:", count);
}, [count]);

// Solution 2: For consecutive updates, use updater callback
setCount(prev => prev + 1);
setCount(prev => prev + 1); // Increments by 2
```

---

### Q4: `useEffect`: Why `useEffect` & Dependency `[]` Array
**Question (From Notes):** Why do we use `useEffect`? Explain dependency array behavior (`[]`, `[dep]`, no array).

**Answer:**
`useEffect` performs side effects (API calls, subscriptions, timers, DOM updates) in functional components.

```jsx
// 1. No dependency array: Runs on EVERY single render
useEffect(() => {
  console.log("Runs on mount and EVERY re-render");
});

// 2. Empty array []: Runs ONCE on initial mount (like componentDidMount)
useEffect(() => {
  console.log("Runs only ONCE after initial mount");
  return () => {
    console.log("Cleanup runs on unmount");
  };
}, []);

// 3. With dependencies [userId]: Runs on mount + whenever 'userId' changes
useEffect(() => {
  console.log("Runs on mount and whenever userId changes:", userId);
  return () => {
    console.log("Cleanup runs before next effect execution or unmount");
  };
}, [userId]);
```

---

### Q5: State Lifting (`stateup lifting`)
**Question (From Notes):** What is Lifting State Up?

**Answer:**
When two or more sibling components need access to the same shared data, you lift the state up to their **closest common parent**. The parent holds the state and passes down the value and callback updaters as props.

```jsx
function App() {
  const [text, setText] = useState("");
  return (
    <div>
      <InputBox value={text} onChange={setText} />
      <DisplayBox text={text} />
    </div>
  );
}
```

---

### Q6: Framework vs Library Difference
**Question (From Notes):** What is the difference between a Framework and a Library (e.g., React vs Angular/Next.js)?

**Answer:**
- **Library (e.g., React)**: A collection of helper functions where **you are in control of the application flow**. You decide routing, state management, and architecture.
- **Framework (e.g., Angular, Next.js)**: Provides an opinionated structure and architecture where **the framework is in control** (Inversion of Control - the framework calls your code).
