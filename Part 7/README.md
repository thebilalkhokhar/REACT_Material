### **48. React Router (v6 and above)**

- **React Router** is the official library for handling navigation in React applications.
- It allows your app to behave like a **Single Page Application (SPA)** — changing the UI without reloading the entire page.
- **Version 6+** introduced a simpler and more declarative syntax.

Installation:

```bash
npm install react-router-dom
```

Usage:

```jsx
import { BrowserRouter, Routes, Route } from "react-router-dom";
import Home from "./Home";
import About from "./About";

function App() {
  return (
    <BrowserRouter>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
```

---

### **49. BrowserRouter, Routes, Route**

These are the **core building blocks** of routing.

- **BrowserRouter:** Wraps your entire app and enables routing via the HTML5 history API.
- **Routes:** A container for all your Route definitions.
- **Route:** Defines the path and component (element) to render.

Example:

```jsx
<BrowserRouter>
  <Routes>
    <Route path="/" element={<Home />} />
    <Route path="/contact" element={<Contact />} />
  </Routes>
</BrowserRouter>
```

✅ `element` prop directly takes a JSX element (no `component={}` in v6).
✅ React Router automatically renders only the first matching route.

---

### **50. useNavigate, useParams, useLocation**

React Router provides **hooks** to handle navigation and routing data.

#### **useNavigate**

Used to navigate programmatically (like `history.push` before v6):

```jsx
import { useNavigate } from "react-router-dom";

function Home() {
  const navigate = useNavigate();
  return <button onClick={() => navigate("/about")}>Go to About</button>;
}
```

#### **useParams**

Access dynamic route parameters:

```jsx
<Route path="/user/:id" element={<User />} />;

function User() {
  const { id } = useParams();
  return <h2>User ID: {id}</h2>;
}
```

#### **useLocation**

Gives the current route’s location object (path, state, key):

```jsx
import { useLocation } from "react-router-dom";

function ShowLocation() {
  const location = useLocation();
  console.log(location.pathname); // e.g., "/about"
  return <p>Current Path: {location.pathname}</p>;
}
```

---

### **51. Nested Routes**

- You can define **routes inside routes**, just like folder structure.
- Useful for dashboards, layouts, or shared navigation bars.

Example:

```jsx
<Routes>
  <Route path="dashboard" element={<Dashboard />}>
    <Route path="profile" element={<Profile />} />
    <Route path="settings" element={<Settings />} />
  </Route>
</Routes>
```

In `Dashboard.jsx`:

```jsx
import { Outlet } from "react-router-dom";

function Dashboard() {
  return (
    <>
      <Navbar />
      <Outlet /> {/* renders nested route here */}
    </>
  );
}
```

---

### **52. Private/Public Routes**

- **Private Routes:** Accessible only if the user is authenticated.
- **Public Routes:** Accessible to everyone.

Example:

```jsx
function PrivateRoute({ children }) {
  const isAuth = localStorage.getItem("token");
  return isAuth ? children : <Navigate to="/login" />;
}

<Routes>
  <Route
    path="/dashboard"
    element={
      <PrivateRoute>
        <Dashboard />
      </PrivateRoute>
    }
  />
</Routes>;
```

✅ Keeps unauthorized users away from protected pages.

---

### **53. Redirects**

- In React Router v6, `Redirect` is replaced by **`<Navigate />`**.
- Used to send users to a new route automatically.

Example:

```jsx
<Route path="/" element={<Navigate to="/home" />} />
```

Or conditionally:

```jsx
{
  isLoggedIn ? <Dashboard /> : <Navigate to="/login" />;
}
```

---

### **54. Dynamic Routing**

- Routes that depend on **data or parameters** rather than fixed paths.
- React Router lets you define routes based on fetched data or props.

Example:

```jsx
const products = [{ id: 1 }, { id: 2 }];

<Routes>
  {products.map((p) => (
    <Route key={p.id} path={`/product/${p.id}`} element={<Product />} />
  ))}
</Routes>;
```

✅ Helps when you have routes generated from APIs (e.g., user profiles, articles).

---

### **55. Lazy Loading Routes**

- For performance optimization — load components **only when needed**.
- Uses React’s `lazy()` and `Suspense`.

Example:

```jsx
import { lazy, Suspense } from "react";
const About = lazy(() => import("./About"));

function App() {
  return (
    <BrowserRouter>
      <Suspense fallback={<p>Loading...</p>}>
        <Routes>
          <Route path="/about" element={<About />} />
        </Routes>
      </Suspense>
    </BrowserRouter>
  );
}
```

✅ Reduces initial bundle size and improves page speed.

---
