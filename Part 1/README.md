## 🧩 **1. Fundamentals**

### **1. What is React and why use it**

- **React** is a JavaScript library (not a framework) developed by **Facebook** for building **user interfaces (UIs)** — especially for single-page applications.
- It helps create **reusable, component-based** UIs that update efficiently when data changes.
- **Why use React:**

  - Fast UI rendering using Virtual DOM.
  - Reusable components reduce code duplication.
  - Huge ecosystem (React Router, Redux, etc.).
  - Backed by a strong community and Facebook.

---

### **2. SPA (Single Page Application) Concept**

- A **Single Page Application (SPA)** loads a single HTML page initially.
- When users navigate, React updates **only specific parts of the page**, instead of reloading the entire page.
- This makes navigation **faster** and gives a **native app-like feel**.
- Example: Gmail, Facebook, or your React app — URL changes but page doesn’t fully reload.

---

### **3. Virtual DOM**

- The **Virtual DOM (VDOM)** is a lightweight **JavaScript copy of the real DOM**.
- When data changes, React:

  1. Updates the virtual DOM.
  2. Compares it with the previous version (**diffing**).
  3. Updates **only the changed parts** in the real DOM (using **reconciliation**).

- This makes React **very fast**, since direct DOM manipulation is expensive.

---

### **4. JSX Syntax and Rules**

- **JSX (JavaScript XML)** lets you write **HTML-like syntax inside JavaScript**.
- Example:

  ```jsx
  const element = <h1>Hello, world!</h1>;
  ```

- Under the hood, JSX gets compiled to:

  ```js
  React.createElement("h1", null, "Hello, world!");
  ```

- **JSX rules:**

  - Must return **one root element**.
  - Use **className** instead of `class`.
  - Expressions go inside **curly braces `{}`**.
  - Use **camelCase** for attributes (e.g., `onClick`, `tabIndex`).

---

### **5. Components (Functional vs Class)**

- React apps are made up of **components** — independent, reusable UI pieces.

**Functional Components:**

```jsx
function Greeting() {
  return <h1>Hello!</h1>;
}
```

- Simpler, use **Hooks** for state and lifecycle logic.

**Class Components (Older Way):**

```jsx
class Greeting extends React.Component {
  render() {
    return <h1>Hello!</h1>;
  }
}
```

- Use `this.state` and lifecycle methods like `componentDidMount`.

➡️ **Modern React uses functional components with Hooks.**

---

### **6. Props and Prop Drilling**

- **Props (Properties)** are used to pass data **from parent to child components**.
- Example:

  ```jsx
  function Welcome(props) {
    return <h1>Hello, {props.name}</h1>;
  }
  ```

- Props are **read-only**; you **cannot modify** them in child components.

**Prop Drilling:**
When props are passed through multiple layers just to reach a deeply nested component.
Solution: **Context API or Redux**.

---

### **7. State and setState**

- **State** represents **data that changes over time** in a component.
- When state changes, React **re-renders** the component.

**Functional Component Example:**

```jsx
import { useState } from "react";

function Counter() {
  const [count, setCount] = useState(0);

  return <button onClick={() => setCount(count + 1)}>Count: {count}</button>;
}
```

- **`useState`** initializes a variable and gives you a function (`setState`) to update it.

---

### **8. Rendering and Re-rendering Process**

- **Initial Render:** React creates the virtual DOM from the JSX and mounts it to the real DOM.
- **Re-render:** Happens when:

  - State or props change.
  - Parent component re-renders.

- React compares the new virtual DOM with the old one (diffing) and updates **only what changed**.

---

### **9. React.createElement() vs JSX**

- JSX is **syntactic sugar** for `React.createElement()`.
- These are equivalent:

  ```jsx
  const element = <h1>Hello</h1>;
  // same as
  const element = React.createElement("h1", null, "Hello");
  ```

- JSX is easier to write and read, but the browser never sees JSX — it’s compiled to `React.createElement()`.

---

### **10. Conditional Rendering**

- Display UI **based on conditions**, just like `if` statements.

**Examples:**

```jsx
{
  isLoggedIn ? <Dashboard /> : <Login />;
}
```

or

```jsx
{
  show && <p>This text is visible only if show is true</p>;
}
```

---

### **11. Lists and Keys**

- You can render lists using the **`map()`** method:

  ```jsx
  const items = ["A", "B", "C"];
  const list = items.map((item, i) => <li key={i}>{item}</li>);
  ```

- **Keys** help React identify which items changed, added, or removed.
- A good **key** should be **unique and stable** (avoid using array index if list can change).

---

### **12. Handling Events in React**

- Events are handled using **camelCase** and pass **functions**, not strings.
- Example:

  ```jsx
  function Button() {
    const handleClick = () => alert("Clicked!");
    return <button onClick={handleClick}>Click me</button>;
  }
  ```

- You can also pass parameters:

  ```jsx
  <button onClick={() => handleClick(id)}>Delete</button>
  ```
