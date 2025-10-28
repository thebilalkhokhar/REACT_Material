## 🧱 **3. Component Communication**

---

### **23. Parent to Child Communication (via Props)**

- The most common type of communication in React.
- The **parent component passes data down to the child** using **props** (short for “properties”).
- Props are **read-only**, meaning the child cannot modify them.

**Example:**

```jsx
function Child({ name }) {
  return <h2>Hello, {name}</h2>;
}

function Parent() {
  return <Child name="Bilal" />;
}
```

**Explanation:**

- `Parent` sends the value `"Bilal"` as a prop named `name`.
- The `Child` receives it as a parameter and displays it.

**Key Rule:**
Props flow **downward only** (from parent → child).
React components are **unidirectional** in data flow.

---

### **24. Child to Parent Communication (via Callbacks)**

- Since data can’t go upward directly, the parent can **pass a callback function** as a prop to the child.
- The **child calls that function** to send data back to the parent.

**Example:**

```jsx
function Child({ onSend }) {
  const message = "Hello from Child!";
  return <button onClick={() => onSend(message)}>Send Message</button>;
}

function Parent() {
  const handleMessage = (msg) => {
    alert("Received: " + msg);
  };

  return <Child onSend={handleMessage} />;
}
```

**Explanation:**

- Parent gives `onSend` (a function) to Child.
- Child executes it with data → Parent receives that data.

**Use Case:**
Useful when child components need to **update parent state** or **trigger parent actions**.

---

### **25. Sibling Communication**

- Sibling components **cannot communicate directly** because they don’t share props or state.
- The solution is to **lift the shared state up** to their **common parent**.

**Example:**

```jsx
function ChildA({ sendData }) {
  return <button onClick={() => sendData("Hello from A")}>Send to B</button>;
}

function ChildB({ data }) {
  return <h3>Message: {data}</h3>;
}

function Parent() {
  const [message, setMessage] = useState("");

  return (
    <>
      <ChildA sendData={setMessage} />
      <ChildB data={message} />
    </>
  );
}
```

**How it works:**

- `ChildA` sends data to `Parent` (via callback).
- `Parent` stores it in state.
- `Parent` passes it down to `ChildB` as a prop.

➡️ So communication becomes:
**Child A → Parent → Child B**

---

### **26. Prop Drilling Problem**

- **Prop Drilling** happens when props are passed **through many intermediate components** just to reach a deeply nested child.
- It makes code **hard to manage** and **less maintainable**.

**Example:**

```jsx
function App() {
  const user = { name: "Bilal" };
  return <Parent user={user} />;
}

function Parent({ user }) {
  return <Child user={user} />;
}

function Child({ user }) {
  return <GrandChild user={user} />;
}

function GrandChild({ user }) {
  return <h2>{user.name}</h2>;
}
```

Here, `user` is passed through **every level** even though only `GrandChild` needs it.
This is inefficient and cluttered — that’s why **Context API** or **Redux** is used.

---

### **27. Context API (Provider & Consumer)**

- The **Context API** is React’s built-in solution to **avoid prop drilling**.
- It allows you to **share data globally** without passing props manually at every level.

**Steps:**

#### Step 1: Create a Context

```jsx
import { createContext } from "react";
export const UserContext = createContext();
```

#### Step 2: Provide the Context

Wrap your component tree with a **Provider** and supply the data.

```jsx
function App() {
  const user = { name: "Bilal" };

  return (
    <UserContext.Provider value={user}>
      <Parent />
    </UserContext.Provider>
  );
}
```

#### Step 3: Consume the Context

Any child component can directly access the context using `useContext()`.

```jsx
import { useContext } from "react";
import { UserContext } from "./App";

function GrandChild() {
  const user = useContext(UserContext);
  return <h2>Hello, {user.name}</h2>;
}
```

**How it helps:**

- No more prop passing through each level.
- Centralized data sharing.
- Best for theme, user info, auth state, etc.

**Components involved:**

- `createContext()` → Creates the context object.
- `Provider` → Makes the data available.
- `useContext()` or `Consumer` → Reads the data.

---

✅ **Summary:**

| Communication Type | Direction | Method              | Use Case                             |
| ------------------ | --------- | ------------------- | ------------------------------------ |
| Parent → Child     | Downward  | Props               | Pass data or functions               |
| Child → Parent     | Upward    | Callback props      | Notify parent or update parent state |
| Sibling ↔ Sibling  | Sideways  | Shared parent state | Share data between siblings          |
| Many-level sharing | Global    | Context API         | Avoid prop drilling                  |

---
