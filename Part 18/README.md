### 🧩 **18. Design Patterns in React**

These patterns define _how to structure components and logic_ for clean, scalable, and maintainable React applications.

---

#### **111. Container–Presenter Pattern**

Also known as the **Smart–Dumb Components Pattern**, it separates _logic_ and _UI_ for cleaner architecture.

- **Container (Smart)** → Handles state, data fetching, and logic
- **Presenter (Dumb)** → Handles only UI and rendering based on props

**Example:**

```jsx
// UserContainer.js
import { useState, useEffect } from "react";
import UserList from "./UserList";

function UserContainer() {
  const [users, setUsers] = useState([]);

  useEffect(() => {
    fetch("/api/users").then(res => res.json()).then(setUsers);
  }, []);

  return <UserList users={users} />;
}
export default UserContainer;

// UserList.js
function UserList({ users }) {
  return (
    <ul>
      {users.map(u => <li key={u.id}>{u.name}</li>)}
    </ul>
  );
}
export default UserList;
```

✅ Benefits:

- Separation of concerns
- Easier testing and reusability
- Clear distinction between data and UI layers

---

#### **112. Hooks Pattern**

A **Hooks pattern** extracts reusable logic (like fetching, form handling, or animations) into **custom hooks**.
This prevents code duplication and keeps components clean.

**Example:**

```jsx
// useFetch.js
import { useState, useEffect } from "react";

function useFetch(url) {
  const [data, setData] = useState(null);
  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then(setData);
  }, [url]);
  return data;
}
export default useFetch;

// App.js
const data = useFetch("/api/products");
```

✅ Benefits:

- Code reuse
- Cleaner component logic
- Improved readability

---

#### **113. Controlled / Uncontrolled Pattern**

This pattern is about managing **form state** and **input behavior**.

- **Controlled Component:** React controls the input value via state.
- **Uncontrolled Component:** DOM manages its own internal state via refs.

**Controlled Example:**

```jsx
function Form() {
  const [value, setValue] = useState("");
  return <input value={value} onChange={(e) => setValue(e.target.value)} />;
}
```

**Uncontrolled Example:**

```jsx
function Form() {
  const inputRef = useRef();
  function handleSubmit() {
    console.log(inputRef.current.value);
  }
  return <input ref={inputRef} />;
}
```

✅ Benefits:

- Controlled → Predictable, good for validation
- Uncontrolled → Simpler, less boilerplate

---

#### **114. State Reducer Pattern**

Used to **customize component logic externally** by passing a reducer function (similar to Redux).
Helps make components flexible without rewriting them.

**Example:**

```jsx
function useToggle(reducer = (state) => !state) {
  const [on, setOn] = useState(false);
  const toggle = () => setOn((prev) => reducer(prev));
  return [on, toggle];
}

// Custom Reducer
const customReducer = (state) => (state ? state : true);
const [on, toggle] = useToggle(customReducer);
```

✅ Benefits:

- Extensible and flexible logic
- Encourages composition
- Used by libraries like Downshift and React Table

---

#### **115. Context Module Pattern**

This pattern organizes **Context API logic** into a single reusable module — separating provider, context, and hook logic.

**Example:**

```jsx
// theme-context.js
import { createContext, useContext, useState } from "react";

const ThemeContext = createContext();

export function ThemeProvider({ children }) {
  const [dark, setDark] = useState(false);
  const toggleTheme = () => setDark((d) => !d);
  return (
    <ThemeContext.Provider value={{ dark, toggleTheme }}>
      {children}
    </ThemeContext.Provider>
  );
}

export const useTheme = () => useContext(ThemeContext);

// App.js
function App() {
  const { dark, toggleTheme } = useTheme();
  return <button onClick={toggleTheme}>{dark ? "Light" : "Dark"}</button>;
}
```

✅ Benefits:

- Centralized global state logic
- Cleaner imports (`useTheme()` instead of `useContext(ThemeContext)`)
- Easier scalability

---
