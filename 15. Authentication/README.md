### **🔐 15. Authentication**

#### **95. JWT Authentication**

**JWT (JSON Web Token)** is a secure way to authenticate users between the frontend and backend.

**Flow:**

1. User logs in → frontend sends credentials to backend
2. Backend validates and sends back a **JWT token**
3. Frontend stores token (in `localStorage` or `httpOnly cookie`)
4. Each API request includes the token in the header:

   ```js
   Authorization: Bearer <token>
   ```

5. Backend verifies the token before giving access

**Example (frontend API call):**

```js
axios.get("/api/user", {
  headers: { Authorization: `Bearer ${localStorage.getItem("token")}` },
});
```

✅ Stateless — no need to store sessions on the server
✅ Portable — works across microservices and mobile

---

#### **96. Context-Based Auth Management**

Instead of passing auth state (like token, user info) manually, use **React Context** to manage it globally.

**Example:**

```tsx
const AuthContext = createContext(null);

export const AuthProvider = ({ children }) => {
  const [user, setUser] = useState(null);
  const login = (userData) => setUser(userData);
  const logout = () => setUser(null);

  return (
    <AuthContext.Provider value={{ user, login, logout }}>
      {children}
    </AuthContext.Provider>
  );
};

export const useAuth = () => useContext(AuthContext);
```

✅ Centralized state for authentication
✅ Easy to access `user` or `logout()` in any component

---

#### **97. Protected Routes**

**Protected routes** restrict access to certain pages unless the user is authenticated.

**Example using React Router:**

```tsx
import { Navigate } from "react-router-dom";
import { useAuth } from "./AuthContext";

function PrivateRoute({ children }) {
  const { user } = useAuth();
  return user ? children : <Navigate to="/login" />;
}
```

Usage:

```tsx
<Route
  path="/dashboard"
  element={
    <PrivateRoute>
      <Dashboard />
    </PrivateRoute>
  }
/>
```

✅ Prevents unauthenticated users from viewing sensitive pages

---

#### **98. Refresh Tokens**

Since JWTs usually **expire quickly** for security, **refresh tokens** are used to get a new access token without forcing the user to log in again.

**Typical flow:**

1. On login → server issues **access token** + **refresh token**
2. Access token is used for API calls (short-lived)
3. When expired → frontend sends refresh token to get a new one

**Example Refresh Logic:**

```js
axios.interceptors.response.use(null, async (error) => {
  if (error.response.status === 401) {
    const res = await axios.post("/auth/refresh", { token: refreshToken });
    localStorage.setItem("token", res.data.accessToken);
  }
});
```

✅ Improves user experience
✅ Maintains security with short-lived access tokens

---

#### **99. Role-Based Access**

You can use roles (e.g. `admin`, `user`, `editor`) to manage access to pages and features.

**Example:**

```tsx
function ProtectedRoute({ children, role }) {
  const { user } = useAuth();
  if (!user) return <Navigate to="/login" />;
  if (role && user.role !== role) return <Navigate to="/unauthorized" />;
  return children;
}
```

Usage:

```tsx
<Route
  path="/admin"
  element={
    <ProtectedRoute role="admin">
      <AdminPanel />
    </ProtectedRoute>
  }
/>
```

✅ Allows granular control over who can access what
✅ Common in dashboards, CMS, and multi-role apps

---
