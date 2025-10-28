### **61. Local Component State**

- Managed directly inside a component using **`useState`** or **`useReducer`**.
- Best for data that affects only a single component.

Example:

```jsx
function Counter() {
  const [count, setCount] = useState(0);
  return (
    <>
      <h2>{count}</h2>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </>
  );
}
```

✅ Pros: Simple and built-in.
❌ Cons: Not scalable — becomes messy when shared across multiple components.

---

### **62. Context API**

- Used to **share state globally** without prop drilling (passing props through multiple levels).
- Good for themes, user data, or authentication.

Example:

```jsx
// 1. Create Context
const ThemeContext = createContext();

// 2. Provide Context
function App() {
  const [theme, setTheme] = useState("light");
  return (
    <ThemeContext.Provider value={{ theme, setTheme }}>
      <Navbar />
    </ThemeContext.Provider>
  );
}

// 3. Consume Context
function Navbar() {
  const { theme, setTheme } = useContext(ThemeContext);
  return (
    <button onClick={() => setTheme(theme === "light" ? "dark" : "light")}>
      Theme: {theme}
    </button>
  );
}
```

✅ Pros: Removes prop drilling, built into React.
❌ Cons: Re-renders all consumers when value changes.

---

### **63. Redux (Core Concepts)**

- A **state container** for managing global app state in a predictable way.
- Based on three main principles:

  1. **Single source of truth** — one global store.
  2. **State is read-only** — changes via actions only.
  3. **Changes are made with pure functions** — reducers.

Example (simple idea):

```jsx
store = {
  count: 0,
};
```

✅ Ideal for large apps needing predictable and traceable state changes.

---

### **64. Actions, Reducers, Store**

- **Action:** Describes what happened (a simple JS object).
- **Reducer:** Pure function that takes the current state and action → returns new state.
- **Store:** Holds the entire state tree.

Example:

```jsx
// Action
const increment = { type: "INCREMENT" };

// Reducer
function counterReducer(state = { count: 0 }, action) {
  switch (action.type) {
    case "INCREMENT":
      return { count: state.count + 1 };
    default:
      return state;
  }
}

// Store
import { createStore } from "redux";
const store = createStore(counterReducer);
```

✅ Predictable, central control over state.

---

### **65. useSelector, useDispatch Hooks**

- Used with **React-Redux** to connect components to the Redux store.

Example:

```jsx
import { useSelector, useDispatch } from "react-redux";

function Counter() {
  const count = useSelector((state) => state.count);
  const dispatch = useDispatch();

  return (
    <>
      <h2>{count}</h2>
      <button onClick={() => dispatch({ type: "INCREMENT" })}>Increment</button>
    </>
  );
}
```

✅ `useSelector` → read data from store
✅ `useDispatch` → send actions to reducers

---

### **66. Redux Toolkit (RTK)**

- A **modern and simplified** way to use Redux.
- Reduces boilerplate with utilities like `createSlice`, `configureStore`, and `createAsyncThunk`.

Example:

```jsx
import { createSlice, configureStore } from "@reduxjs/toolkit";

const counterSlice = createSlice({
  name: "counter",
  initialState: { value: 0 },
  reducers: {
    increment: (state) => {
      state.value += 1;
    },
  },
});

export const { increment } = counterSlice.actions;
export const store = configureStore({ reducer: counterSlice.reducer });
```

✅ Pros: Cleaner, faster, and supports async logic out of the box.

---

### **67. RTK Query**

- A powerful data-fetching and caching tool built into Redux Toolkit.
- Handles **API calls**, **loading**, **error**, and **caching** automatically.

Example:

```jsx
import { createApi, fetchBaseQuery } from "@reduxjs/toolkit/query/react";

export const usersApi = createApi({
  reducerPath: "usersApi",
  baseQuery: fetchBaseQuery({ baseUrl: "/api" }),
  endpoints: (builder) => ({
    getUsers: builder.query({
      query: () => "/users",
    }),
  }),
});

export const { useGetUsersQuery } = usersApi;
```

Usage:

```jsx
function Users() {
  const { data, isLoading } = useGetUsersQuery();
  if (isLoading) return <p>Loading...</p>;
  return (
    <ul>
      {data.map((u) => (
        <li key={u.id}>{u.name}</li>
      ))}
    </ul>
  );
}
```

✅ Pros: Replaces Axios + Redux combo, automatic caching & invalidation.
✅ Great for API-heavy applications.

---

### **68. Zustand, Recoil, or Jotai (Alternatives)**

These are **modern lightweight state management libraries** that simplify React state handling.

#### **🪴 Zustand**

- Minimal and fast.
- No boilerplate — just create a store and use it.

```jsx
import { create } from "zustand";

const useStore = create((set) => ({
  count: 0,
  increment: () => set((s) => ({ count: s.count + 1 })),
}));

function Counter() {
  const { count, increment } = useStore();
  return <button onClick={increment}>{count}</button>;
}
```

#### **⚛️ Recoil**

- Developed by Facebook.
- Atom-based global state — reactive and simple.

```jsx
import { atom, useRecoilState } from "recoil";

const countAtom = atom({ key: "count", default: 0 });

function Counter() {
  const [count, setCount] = useRecoilState(countAtom);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

#### **🔹 Jotai**

- Primitive and minimal — each atom is a single piece of state.

```jsx
import { atom, useAtom } from "jotai";

const countAtom = atom(0);

function Counter() {
  const [count, setCount] = useAtom(countAtom);
  return <button onClick={() => setCount(count + 1)}>{count}</button>;
}
```

✅ Pros (for all three): Lightweight, no boilerplate, fast updates.
✅ Perfect for medium-scale apps or when Redux feels heavy.

---
