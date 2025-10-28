### **33. Controlled vs Uncontrolled Components**

- **Controlled Components:**
  These are form elements (like input, textarea, select) whose values are controlled by React **state**.

  - Example:

    ```jsx
    function Form() {
      const [name, setName] = useState("");
      return <input value={name} onChange={(e) => setName(e.target.value)} />;
    }
    ```

  - React fully controls the input value through `useState`.

- **Uncontrolled Components:**
  Here, the form element maintains its own state internally. You use a **ref** to access its value.

  - Example:

    ```jsx
    function Form() {
      const inputRef = useRef();
      const handleSubmit = () => alert(inputRef.current.value);
      return <input ref={inputRef} />;
    }
    ```

  - Useful when you don’t need to track input value on every keystroke.

---

### **34. Higher-Order Components (HOC)**

- A **Higher-Order Component** is a function that takes a component as an argument and returns a new component with additional functionality.
- It’s a pattern for **code reuse and logic sharing** before hooks were introduced.

Example:

```jsx
function withLogger(WrappedComponent) {
  return function (props) {
    console.log("Rendering", WrappedComponent.name);
    return <WrappedComponent {...props} />;
  };
}

const Enhanced = withLogger(MyComponent);
```

Use cases: Authentication checks, logging, analytics, permission handling.

---

### **35. Render Props**

- A **render prop** is a technique to share logic between components using a **function as a prop**.

Example:

```jsx
function MouseTracker({ render }) {
  const [pos, setPos] = useState({ x: 0, y: 0 });
  return (
    <div onMouseMove={(e) => setPos({ x: e.clientX, y: e.clientY })}>
      {render(pos)}
    </div>
  );
}

<MouseTracker
  render={({ x, y }) => (
    <h1>
      {x}, {y}
    </h1>
  )}
/>;
```

Here, the parent decides how to render data — not the component itself.

---

### **36. Compound Components**

- A pattern that lets components **work together** through an implicit shared state.
- Often used in libraries like `React-Select` or `Headless UI`.

Example:

```jsx
function Toggle({ children }) {
  const [on, setOn] = useState(false);
  return React.Children.map(children, (child) =>
    React.cloneElement(child, { on, setOn })
  );
}

Toggle.On = ({ on, children }) => (on ? children : null);
Toggle.Off = ({ on, children }) => (!on ? children : null);
Toggle.Button = ({ on, setOn }) => (
  <button onClick={() => setOn(!on)}>{on ? "ON" : "OFF"}</button>
);

<Toggle>
  <Toggle.On>Light On</Toggle.On>
  <Toggle.Off>Light Off</Toggle.Off>
  <Toggle.Button />
</Toggle>;
```

---

### **37. Portals**

- **Portals** allow rendering a component’s content into a **different part of the DOM tree**.
- Common use case: Modals, tooltips, or dropdowns that need to escape parent CSS overflow or z-index restrictions.

Example:

```jsx
import { createPortal } from "react-dom";

function Modal({ children }) {
  return createPortal(children, document.getElementById("modal-root"));
}
```

---

### **38. Error Boundaries**

- Error boundaries catch **JavaScript errors** in child components and prevent the app from crashing.
- Implemented using **class components** with `componentDidCatch` and `getDerivedStateFromError`.

Example:

```jsx
class ErrorBoundary extends React.Component {
  state = { hasError: false };
  static getDerivedStateFromError() {
    return { hasError: true };
  }
  componentDidCatch(error, info) {
    console.log(error, info);
  }
  render() {
    return this.state.hasError ? (
      <h2>Something went wrong</h2>
    ) : (
      this.props.children
    );
  }
}
```

---

### **39. Reconciliation**

- Reconciliation is React’s **diffing algorithm** — how React decides what parts of the UI need to be updated.
- React compares the **Virtual DOM** of the previous render with the new one, and only updates what’s changed.
- It uses **keys** to efficiently track items in lists.

Example:

```jsx
<ul>
  {items.map((item) => (
    <li key={item.id}>{item.name}</li>
  ))}
</ul>
```

If keys are missing or unstable, React may re-render incorrectly.

---

### **40. Fiber Architecture**

- **React Fiber** is the internal engine that powers React since v16.
- It breaks rendering work into **small chunks (units of work)** so that React can pause and resume rendering.
- Enables **features like concurrent rendering, Suspense, and transitions**.
- Think of Fiber as the brain that schedules and prioritizes UI updates smoothly.

---

### **41. Strict Mode**

- A **development-only tool** that highlights potential problems (not active in production).
- Helps detect unsafe lifecycle methods, side effects, and deprecated APIs.

Example:

```jsx
<React.StrictMode>
  <App />
</React.StrictMode>
```

It may cause double-rendering of components in development — that’s intentional to detect side effects.
