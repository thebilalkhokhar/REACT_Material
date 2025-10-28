### 🧑‍💻 **19. Common Interview Topics**

These are the **most frequently asked React interview concepts**, and mastering them will give you a strong edge in technical interviews.

---

#### **116. Lifecycle Methods (Class vs Hooks)**

**Class Components Lifecycle Phases:**

1. **Mounting** – When component is created
   → `constructor()`, `componentDidMount()`
2. **Updating** – When props or state changes
   → `componentDidUpdate()`
3. **Unmounting** – When component is removed
   → `componentWillUnmount()`

**Hooks Equivalent:**

- `useEffect(() => {}, [])` → `componentDidMount`
- `useEffect(() => {...})` → `componentDidUpdate`
- `useEffect(() => { return cleanup })` → `componentWillUnmount`

**Example:**

```jsx
useEffect(() => {
  console.log("Mounted");
  return () => console.log("Unmounted");
}, []);
```

---

#### **117. Difference Between Props and State**

| Feature    | Props                                | State                                              |
| ---------- | ------------------------------------ | -------------------------------------------------- |
| Definition | Data passed **from parent to child** | Data **managed within** a component                |
| Mutability | Immutable (read-only)                | Mutable (can change with `setState` or `useState`) |
| Ownership  | Parent controls it                   | Component controls it                              |
| Use case   | Configuration / input                | Internal UI behavior                               |

**Example:**

```jsx
function Child({ name }) {
  // props
  const [count, setCount] = useState(0); // state
}
```

---

#### **118. Controlled vs Uncontrolled Components**

- **Controlled:** React state is the single source of truth
- **Uncontrolled:** DOM handles input’s own internal state via refs

**Controlled Example:**

```jsx
<input value={name} onChange={(e) => setName(e.target.value)} />
```

**Uncontrolled Example:**

```jsx
<input ref={inputRef} />
```

✅ Controlled → Easier validation & debugging
✅ Uncontrolled → Simpler for quick use cases

---

#### **119. Virtual DOM vs Real DOM**

| Concept     | Virtual DOM                                  | Real DOM                        |
| ----------- | -------------------------------------------- | ------------------------------- |
| Type        | In-memory lightweight copy                   | Actual browser DOM              |
| Performance | Fast updates via diffing                     | Slower, requires full re-render |
| Updating    | React compares (diffs) & updates efficiently | Direct DOM manipulation         |
| Purpose     | Optimize UI rendering                        | Render actual elements          |

🧠 **React flow:**
Render → Virtual DOM → Diff → Update Real DOM efficiently

---

#### **120. useEffect Dependency Array Behavior**

The **dependency array** determines when `useEffect` runs:

- `useEffect(() => {...}, [])` → Runs **once** after mount
- `useEffect(() => {...}, [count])` → Runs when `count` changes
- `useEffect(() => {...})` → Runs **after every render**

**Example:**

```jsx
useEffect(() => {
  console.log("Count changed:", count);
}, [count]);
```

🚫 Common Mistake: Forgetting dependencies causes stale data or missing updates.

---

#### **121. Why Keys Are Important in Lists**

React uses **keys** to identify which list items have changed, been added, or removed.

**Without keys:** React re-renders all items unnecessarily
**With keys:** React reuses and efficiently updates only changed items

**Example:**

```jsx
{
  users.map((user) => <li key={user.id}>{user.name}</li>);
}
```

✅ Keys must be **unique and stable** (avoid using index if list changes).

---

#### **122. Difference Between Context API and Redux**

| Feature     | Context API                               | Redux                                    |
| ----------- | ----------------------------------------- | ---------------------------------------- |
| Purpose     | Share data globally (simple global state) | Complex global state management          |
| Setup       | Simple (built into React)                 | Requires setup, store, reducers, actions |
| Performance | May cause re-renders                      | Optimized with selectors                 |
| Best for    | Theme, auth, language                     | Large apps, multiple data sources        |

👉 **Rule of thumb:**

- Small app → Context API
- Scalable app → Redux / Zustand / RTK

---

#### **123. Performance Optimization Techniques**

1. **Memoization:** `React.memo`, `useMemo`, `useCallback`
2. **Code Splitting:** Lazy load components using `React.lazy`
3. **Virtualization:** `react-window`, `react-virtualized`
4. **Avoid unnecessary re-renders** with correct key and props usage
5. **Profiler** to analyze render performance
6. **Debounce / Throttle** expensive operations

---

#### **124. SSR vs CSR vs SSG**

| Rendering Type                   | Description                                 | Framework Example |
| -------------------------------- | ------------------------------------------- | ----------------- |
| **CSR (Client-Side Rendering)**  | Rendering happens in browser after JS loads | React (default)   |
| **SSR (Server-Side Rendering)**  | HTML rendered on server and sent to client  | Next.js SSR       |
| **SSG (Static Site Generation)** | HTML generated at build time                | Next.js SSG       |

✅ SSR → SEO + Dynamic
✅ SSG → Fast + Cached
✅ CSR → Interactive + SPA feel

---

#### **125. React 19 New Features (Upcoming / Experimental)**

🚀 **React 19 introduces next-gen improvements** for async and server actions:

- **`useOptimistic`** → Optimistic UI updates before server confirmation
- **`useActionState`** → Manages async form state (pending, success, error)
- **`useFormStatus`** → Check submission state in form components
- **Server Actions** → Call async functions directly from UI (no client fetch required)
- **Automatic Script Loading** & **Improved Suspense** handling

**Example:**

```jsx
const [optimisticCount, addOptimisticCount] = useOptimistic(
  count,
  (c) => c + 1
);
```

✅ Less boilerplate for async tasks
✅ Smoother UI interactions
✅ Native support for modern server-driven apps

---
