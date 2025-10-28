### **⚡ 11. Performance Optimization**

#### **74. React.memo**

`React.memo` is a **higher-order component (HOC)** that prevents unnecessary re-renders of functional components.
It re-renders the component **only if its props change.**

**Example:**

```js
const Child = React.memo(({ value }) => {
  console.log("Child rendered");
  return <p>{value}</p>;
});

function App() {
  const [count, setCount] = useState(0);
  return (
    <>
      <Child value="Static Text" />
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

🧠 Even if the parent re-renders, `Child` won’t unless its `value` prop changes.

---

#### **75. useMemo & useCallback**

Both are React hooks that **cache values or functions** to avoid unnecessary recalculations or re-creations.

- **useMemo:**
  Caches the **result of a computation**.

  ```js
  const expensiveValue = useMemo(() => {
    return heavyComputation(num);
  }, [num]);
  ```

  ✅ Useful for expensive calculations that don’t need to run every render.

- **useCallback:**
  Caches the **function definition** to prevent it from being recreated on each render.

  ```js
  const handleClick = useCallback(() => {
    console.log("Clicked");
  }, []);
  ```

  ✅ Useful when passing callbacks to memoized child components.

---

#### **76. Code Splitting and Lazy Loading**

To improve load performance, React lets you **split your app into smaller bundles** and **load them on demand**.

- **Dynamic Import Example:**

  ```js
  const Dashboard = React.lazy(() => import("./Dashboard"));
  ```

- **Usage:**

  ```js
  <Suspense fallback={<p>Loading...</p>}>
    <Dashboard />
  </Suspense>
  ```

✅ Only loads `Dashboard` when needed, reducing the initial bundle size.

---

#### **77. Suspense**

`Suspense` lets React **wait for something** (like lazy-loaded components or async data) before rendering.

**Example:**

```js
<Suspense fallback={<div>Loading component...</div>}>
  <LazyComponent />
</Suspense>
```

🧠 Often used with **React.lazy()** or **data fetching libraries** (like React Query or Relay).

---

#### **78. Avoiding Unnecessary Re-renders**

Unnecessary re-renders slow down your app. You can reduce them by:

- Using **React.memo** for pure functional components.
- Keeping **state local** to components that actually need it.
- Using **key props** wisely in lists.
- Avoiding **inline functions/objects** (use `useCallback` or `useMemo`).
- Splitting large components into smaller reusable parts.

---

#### **79. React Profiler**

**React Profiler** is a developer tool to measure the performance of React components — i.e., how often they render and why.

You can find it in the **React Developer Tools** extension in Chrome/Firefox.

**It helps identify:**

- Components causing frequent re-renders
- Long render times
- Inefficient component hierarchies

Example Usage (programmatic profiling):

```js
import { Profiler } from "react";

<Profiler id="App" onRender={(...data) => console.log(data)}>
  <App />
</Profiler>;
```

---
