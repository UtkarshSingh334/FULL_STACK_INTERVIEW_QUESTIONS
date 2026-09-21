# ⚛️ React - Easy & Core Fundamentals

> **Topics Covered:** What is React & Why is it a Library?, JSX Compilation, Virtual DOM vs Real DOM, Reconciliation, Component Lifecycle (Mounting, Updating, Unmounting), What Causes Re-Renders, Props vs State, Props Immutability, Prop Drilling & Composition, Keys & Array Index as Key Anti-Pattern, Controlled vs Uncontrolled Components.

---

### Q1: What is React and Why is it Called a Library, Not a Framework?
**Question:** What is React? Why is it classified as a library rather than a full-fledged framework like Angular?

**Answer:**
- **React** is an open-source, component-driven JavaScript library for building user interfaces, maintained by Meta.
- **Library vs Framework:**
  - **Framework (e.g. Angular, Django)**: Opinionated "all-in-one" solution that dictates project structure, routing, HTTP fetching, state management, and build tools. "The framework calls your code."
  - **Library (React)**: Unopinionated UI layer. Focuses strictly on rendering the view layer ($V$ in MVC). You have the flexibility to choose your own libraries for routing (React Router), state (Redux/Zustand), and data fetching (React Query/Axios). "Your code calls the library."

---

### Q2: What is JSX and How Does It Get Converted into JavaScript?
**Question:** What is JSX? How does the browser execute JSX?

**Answer:**
- **JSX (JavaScript XML)** is a syntax extension that lets you write HTML-like markup directly inside JavaScript files.
- **Transpilation Flow:** Browsers do not understand JSX. During the build process, compilers like **Babel** or **SWC** transpile JSX tags into `React.createElement()` or `_jsx()` function calls which evaluate to plain JavaScript objects (Virtual DOM nodes).

```jsx
// JSX Source:
const element = <button className="btn" onClick={handleClick}>Click Me</button>;

// Transpiled JavaScript (Babel):
const element = React.createElement(
  "button",
  { className: "btn", onClick: handleClick },
  "Click Me"
);
```

---

### Q3: Virtual DOM vs Real DOM & Reconciliation
**Question:** What is the Virtual DOM? How does it differ from the Real DOM, and what is Reconciliation?

**Answer:**
- **Real DOM**: The browser's native tree representation of the UI. Updating Real DOM nodes is computationally expensive because changes trigger browser layout recalculations (Reflow) and Repaints.
- **Virtual DOM (VDOM)**: A lightweight, in-memory JavaScript object representation of the Real DOM.
- **Reconciliation (The Diffing Algorithm)**:
  1. When state or props change, React creates a new VDOM tree.
  2. React compares the new VDOM with the previous VDOM snapshot using an optimized $O(n)$ heuristic algorithm.
  3. React computes the exact minimal set of changes (patches) and batches them into the Real DOM in a single update.

---

### Q4: What Causes a React Component to Re-render?
**Question:** What are all the triggers that cause a React component to re-render?

**Answer:**
A component re-renders when:
1. **State Changes**: Calling `setState()` / `useState` setter with a new reference.
2. **Props Change**: Parent passes new or changed prop values.
3. **Parent Re-renders**: By default, when a parent component re-renders, all its child components re-render recursively (unless memoized via `React.memo`).
4. **Context Value Changes**: Any component consuming a Context via `useContext` re-renders when the Provider's `value` updates.
5. **Hooks Trigger**: Custom hooks or internal hooks dispatching state updates.

---

### Q5: Component Lifecycle Phases: Mounting, Updating, Unmounting
**Question:** What are the three phases of a React component lifecycle? How do functional hooks map to them?

**Answer:**
1. **Mounting**: Component instance is created and inserted into the DOM.
   - *Class:* `componentDidMount()`
   - *Hook:* `useEffect(() => { ... }, [])`
2. **Updating**: Triggered by state or prop changes.
   - *Class:* `componentDidUpdate(prevProps, prevState)`
   - *Hook:* `useEffect(() => { ... }, [dependencies])`
3. **Unmounting**: Component is removed from the DOM.
   - *Class:* `componentWillUnmount()`
   - *Hook:* `useEffect(() => { return () => { /* cleanup */ }; }, [])`

---

### Q6: Why are Props Immutable in React?
**Question:** Why are props read-only? What happens if you try to modify `props.title = "New"`?

**Answer:**
- **Pure Function Principle**: React requires components to act like pure functions with respect to their props.
- **Predictable Data Flow**: If child components mutated parent props directly, child components would unpredictably alter state across sibling components, creating untraceable bugs and breaking unidirectional data flow.
- Modifying props directly causes unexpected state corruption and throws errors in strict mode.

---

### Q7: Prop Drilling vs Component Composition
**Question:** What is Prop Drilling and how does Component Composition solve it without Context API?

**Answer:**
- **Prop Drilling**: Passing data through multiple intermediary components that do not need the data, solely to reach a deeply nested child.
- **Component Composition Solution**: Pass the child component itself as a prop (`children`) so the parent directly injects the required data.

```jsx
// Instead of Prop Drilling user to Layout -> Sidebar -> Profile:
function App() {
  const user = { name: "Utkarsh" };
  return (
    <Layout sidebar={<Profile user={user} />}>
      <MainContent />
    </Layout>
  );
}
```

---

### Q8: Keys in React: Why is Array Index Dangerous as a Key?
**Question:** Why does React require a `key` prop on list items? Why should you avoid `key={index}`?

**Answer:**
- **Role of Keys**: Keys provide a stable identity across renders so React's diffing algorithm knows whether an item was added, removed, or reordered.
- **Why Index Key Fails**: If you delete or insert items at the beginning/middle of a list, the indices of existing items shift. React will mistakenly associate old state (e.g. checkbox selections, input text) with newly positioned items, causing serious UI corruption.

```jsx
// ❌ Bad:
{items.map((item, index) => <TodoItem key={index} todo={item} />)}

// ✅ Correct:
{items.map(item => <TodoItem key={item.id} todo={item} />)}
```
