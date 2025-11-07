### **🌍 10. API Integration**

#### **69. Fetch API & Axios**

- **Fetch API:**
  A built-in JavaScript method to make HTTP requests (GET, POST, PUT, DELETE, etc.).
  Example:

  ```js
  useEffect(() => {
    fetch("https://api.example.com/data")
      .then((res) => res.json())
      .then((data) => setData(data));
  }, []);
  ```

- **Axios:**
  A popular external library that simplifies HTTP requests and automatically parses JSON.
  Example:

  ```js
  import axios from "axios";
  useEffect(() => {
    axios.get("https://api.example.com/data").then((res) => setData(res.data));
  }, []);
  ```

🧠 _Axios handles errors and interceptors more elegantly than fetch._

---

#### **70. Async/Await with useEffect**

When using async/await in a functional component, you can’t make the `useEffect` callback itself async — but you can define an async function inside it.

Example:

```js
useEffect(() => {
  const fetchData = async () => {
    try {
      const res = await fetch("https://api.example.com/data");
      const json = await res.json();
      setData(json);
    } catch (err) {
      console.error(err);
    }
  };
  fetchData();
}, []);
```

✅ Cleaner syntax
✅ Easier error handling with try/catch

---

#### **71. Handling Loading & Error States**

Always track **3 key states** when making API calls:

1. **Loading** → show spinner or skeleton
2. **Success (Data)** → render fetched data
3. **Error** → display error message

Example:

```js
const [loading, setLoading] = useState(true);
const [error, setError] = useState(null);

useEffect(() => {
  const getData = async () => {
    try {
      const res = await fetch("https://api.example.com/data");
      const json = await res.json();
      setData(json);
    } catch (err) {
      setError(err.message);
    } finally {
      setLoading(false);
    }
  };
  getData();
}, []);
```

---

#### **72. Global API Management**

For managing APIs **globally** (beyond local component state), you can use:

- **Redux Thunk:**
  A middleware allowing async logic in Redux actions.
  Example:

  ```js
  export const fetchUsers = () => async (dispatch) => {
    const res = await fetch("/users");
    const data = await res.json();
    dispatch({ type: "SET_USERS", payload: data });
  };
  ```

- **RTK Query (Redux Toolkit Query):**
  A modern alternative that automatically handles caching, refetching, and loading states.
  Example:

  ```js
  const { data, error, isLoading } = useGetUsersQuery();
  ```

- **React Query (TanStack Query):**
  A library for server-state management that makes API handling simple and efficient.
  Example:

  ```js
  const { data, error, isLoading } = useQuery("users", fetchUsers);
  ```

---

#### **73. useSWR / React Query for Caching**

These libraries automatically handle:

- Data caching
- Background revalidation
- Refetching on window focus
- Error retries

**SWR Example:**

```js
import useSWR from "swr";

const fetcher = (url) => fetch(url).then((res) => res.json());

function App() {
  const { data, error, isLoading } = useSWR("/api/data", fetcher);
}
```

**React Query Example:**

```js
import { useQuery } from "@tanstack/react-query";

function App() {
  const { data, isLoading, error } = useQuery({
    queryKey: ["data"],
    queryFn: () => fetch("/api/data").then((res) => res.json()),
  });
}
```

---
