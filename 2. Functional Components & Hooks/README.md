## ⚙️ **2. Functional Components & Hooks**

React **Hooks** are special functions that let you **“hook into” React’s features** — like state, lifecycle, and context — directly in **functional components** (without needing class components).

They were introduced in **React 16.8** and now are the **modern standard** for all new React apps.

---

### **13. useState Hook**

- `useState` lets you **add state** to a functional component.
- It returns a **state variable** and a **function** to update that state.

**Example:**

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0); // initial value = 0

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increase</button>
    </div>
  );
}
```

**Key points:**

- Changing state triggers **re-render**.
- State updates are **asynchronous** (React batches them).
- Always **use the updater function** (`setCount`) — never mutate directly (`count++` ❌).

---

### **14. useEffect Hook**

- `useEffect` lets you **run side effects** in functional components — like:

  - Fetching data from APIs
  - Subscribing to events
  - Updating the document title

**Syntax:**

```jsx
useEffect(() => {
  // effect code here
  return () => {
    // cleanup (optional)
  };
}, [dependencies]);
```

**Example:**

```jsx
useEffect(() => {
  console.log("Component mounted");
  return () => console.log("Component unmounted");
}, []);
```

**Dependency array behavior:**

- `[]` → runs only once (on mount)
- `[state]` → runs when `state` changes
- no array → runs on **every render**

---

### **15. useRef Hook**

- `useRef` creates a **mutable reference** that **does not cause re-renders** when updated.
- Common uses:

  1. Accessing **DOM elements** directly.
  2. Storing **mutable values** (like previous states or timers).

**Example 1 – Accessing DOM:**

```jsx
import { useRef, useEffect } from "react";

function InputFocus() {
  const inputRef = useRef(null);

  useEffect(() => {
    inputRef.current.focus();
  }, []);

  return <input ref={inputRef} placeholder="Focuses on mount" />;
}
```

**Example 2 – Storing values:**

```jsx
const countRef = useRef(0);
countRef.current += 1; // does not trigger re-render
```

---

### **16. useMemo Hook**

- `useMemo` **memoizes (caches)** a computed value to **avoid expensive recalculations** on every render.

**Example:**

```jsx
import { useMemo, useState } from "react";

function ExpensiveCalc({ number }) {
  const [count, setCount] = useState(0);

  const square = useMemo(() => {
    console.log("Calculating...");
    return number * number;
  }, [number]); // only recalculates if number changes

  return (
    <>
      <p>Square: {square}</p>
      <button onClick={() => setCount(count + 1)}>Re-render</button>
    </>
  );
}
```

**When to use:**
Only for **expensive calculations** or **derived data** — not for every simple variable.

---

### **17. useCallback Hook**

- `useCallback` **memoizes a function**, preventing it from being recreated on every render.
- Useful when passing functions as **props** to child components (to avoid unnecessary re-renders).

**Example:**

```jsx
import { useCallback, useState } from "react";

function Parent() {
  const [count, setCount] = useState(0);

  const handleClick = useCallback(() => {
    console.log("Button clicked!");
  }, []); // same function reference every render

  return (
    <>
      <button onClick={() => setCount(count + 1)}>Increase</button>
      <Child onClick={handleClick} />
    </>
  );
}

function Child({ onClick }) {
  console.log("Child rendered");
  return <button onClick={onClick}>Click Child</button>;
}
```

---

### **18. useContext Hook**

- `useContext` allows you to **use data from Context API** directly, without prop drilling.

**Step 1 – Create Context:**

```jsx
import { createContext } from "react";
export const ThemeContext = createContext();
```

**Step 2 – Provide Context:**

```jsx
<ThemeContext.Provider value="dark">
  <App />
</ThemeContext.Provider>
```

**Step 3 – Consume Context:**

```jsx
import { useContext } from "react";
import { ThemeContext } from "./ThemeContext";

function Button() {
  const theme = useContext(ThemeContext);
  return <button className={theme}>Click</button>;
}
```

---

### **19. useReducer Hook**

- `useReducer` is an **alternative to useState** for complex state logic.
- It’s based on **Redux-style reducers**.

**Syntax:**

```jsx
const [state, dispatch] = useReducer(reducer, initialState);
```

**Example:**

```jsx
function reducer(state, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    case "DECREMENT":
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <>
      <p>{state.count}</p>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>+</button>
      <button onClick={() => dispatch({ type: "DECREMENT" })}>-</button>
    </>
  );
}
```

**When to use:**
When state logic involves **multiple sub-values** or **complex updates**.

---

### **20. useLayoutEffect Hook**

- Similar to `useEffect`, but it runs **synchronously after all DOM mutations** (before browser paint).
- Use it for operations that **must happen before the screen updates**, such as:

  - Measuring DOM elements.
  - Adjusting layout instantly.

**Example:**

```jsx
useLayoutEffect(() => {
  console.log("Runs before browser paint");
});
```

⚠️ **Tip:**
Use `useLayoutEffect` **only when necessary** — it can block the UI if misused.

---

### **21. useImperativeHandle Hook**

- Used **with `forwardRef()`** to **control what values/functions a parent can access** through a ref.
- Helps expose a **custom API** from a child component.

**Example:**

```jsx
import { useImperativeHandle, useRef, forwardRef } from "react";

const Input = forwardRef((props, ref) => {
  const inputRef = useRef();

  useImperativeHandle(ref, () => ({
    focusInput() {
      inputRef.current.focus();
    },
  }));

  return <input ref={inputRef} />;
});

function Parent() {
  const ref = useRef();

  return (
    <>
      <Input ref={ref} />
      <button onClick={() => ref.current.focusInput()}>Focus Input</button>
    </>
  );
}
```

---

### **22. Custom Hooks (Creating & Reusing)**

- A **Custom Hook** is simply a function that uses one or more React hooks.
- It allows you to **reuse logic** between components.

**Example:**

```jsx
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then((data) => setData(data));
  }, [url]);

  return data;
}
```

**Usage:**

```jsx
function Users() {
  const users = useFetch("https://jsonplaceholder.typicode.com/users");
  return <pre>{JSON.stringify(users, null, 2)}</pre>;
}
```

**Rules of Hooks:**

1. Only call hooks **at the top level** (not inside loops or conditions).
2. Only call hooks **from React functions** (components or custom hooks).

---
