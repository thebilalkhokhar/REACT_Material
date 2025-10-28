### **🧮 14. TypeScript with React**

#### **90. Props & State Typing**

In TypeScript, you define the **shape (type)** of props and state to prevent bugs.

**Example — Typing Props:**

```tsx
type UserProps = {
  name: string;
  age?: number; // optional
};

const UserCard: React.FC<UserProps> = ({ name, age }) => (
  <div>
    {name} - {age}
  </div>
);
```

**Example — Typing State:**

```tsx
const [count, setCount] = useState<number>(0);
const [user, setUser] = useState<{ name: string; email: string } | null>(null);
```

✅ Prevents passing wrong types
✅ Improves autocomplete and intellisense

---

#### **91. Generics in Components**

**Generics** allow you to create **reusable components** that can accept different data types dynamically.

**Example:**

```tsx
type ListProps<T> = {
  items: T[];
  render: (item: T) => JSX.Element;
};

function List<T>({ items, render }: ListProps<T>) {
  return <ul>{items.map(render)}</ul>;
}

// Usage:
<List items={[1, 2, 3]} render={(num) => <li>{num}</li>} />;
<List items={["A", "B"]} render={(letter) => <li>{letter}</li>} />;
```

✅ Adds flexibility while maintaining type safety

---

#### **92. Custom Hook Typing**

When creating custom hooks, you should define both input and output types.

**Example:**

```tsx
function useFetch<T>(url: string): {
  data: T | null;
  loading: boolean;
  error: string | null;
} {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<string | null>(null);

  useEffect(() => {
    fetch(url)
      .then((res) => res.json())
      .then(setData)
      .catch((err) => setError(err.message))
      .finally(() => setLoading(false));
  }, [url]);

  return { data, loading, error };
}
```

✅ Hook can fetch any data type while staying type-safe.

---

#### **93. Context Typing**

When using React Context with TypeScript, define the context value type to avoid runtime errors.

**Example:**

```tsx
type ThemeContextType = {
  theme: "light" | "dark";
  toggleTheme: () => void;
};

const ThemeContext = createContext<ThemeContextType | null>(null);

export const useTheme = () => {
  const context = useContext(ThemeContext);
  if (!context) throw new Error("useTheme must be used within ThemeProvider");
  return context;
};
```

✅ Prevents accessing undefined values
✅ Enforces consistent context usage

---

#### **94. Component Type Inference**

React can **infer types automatically** for props, events, and JSX without explicit annotation.

**Example:**

```tsx
const Button = ({
  onClick,
}: {
  onClick: (e: React.MouseEvent<HTMLButtonElement>) => void;
}) => <button onClick={onClick}>Click</button>;
```

Or more simply, by using **React.FC**:

```tsx
const Button: React.FC<{ label: string }> = ({ label }) => (
  <button>{label}</button>
);
```

🧠 However, explicit typing is often better for clarity in larger projects.

---
