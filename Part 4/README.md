## 🧭 **4. Project Structure & Workflow**

---

### **28. Folder Structure Best Practices**

A well-organized folder structure keeps your React project **easy to navigate** and **scalable** as it grows.

Here’s a commonly used and clean structure for React apps (especially with Vite or CRA):

```
src/
│
├── assets/             # Images, icons, fonts, etc.
├── components/         # Reusable UI components (Button, Card, Navbar)
├── pages/              # Page-level components (Home, About, Profile)
├── layouts/            # Shared layouts (Sidebar + Navbar wrappers)
├── context/            # React Context providers (AuthContext, ThemeContext)
├── hooks/              # Custom hooks (useAuth, useFetch, useTheme)
├── services/           # API calls or external integrations
├── utils/              # Helper functions, formatters, constants
├── styles/             # Global CSS, Tailwind, SCSS, etc.
├── App.jsx             # Root component
├── main.jsx            # Entry point (renders App)
└── index.css           # Global styles
```

**Benefits of this structure:**

- Keeps logic, UI, and data separated.
- Makes reusability and maintenance easier.
- Follows a **feature-based modular approach**.

**Tip:**
For large-scale apps, you can even group files by _feature/module_ instead of type, like:

```
src/features/
   ├── auth/
   │   ├── Login.jsx
   │   ├── Signup.jsx
   │   ├── authService.js
   │   └── authSlice.js
   ├── products/
   │   ├── ProductList.jsx
   │   ├── ProductCard.jsx
   │   └── productService.js
```

---

### **29. React Scripts and npm/yarn Commands**

React projects (especially ones created with **Create React App** or **Vite**) use scripts defined in `package.json` for development and production tasks.

**Common Commands:**

| Command                        | Description                                     |
| ------------------------------ | ----------------------------------------------- |
| `npm start` / `yarn start`     | Starts the development server                   |
| `npm run build` / `yarn build` | Creates optimized production build              |
| `npm test`                     | Runs unit tests                                 |
| `npm run eject`                | Exposes internal configurations (only in CRA)   |
| `npm install <package>`        | Installs a dependency                           |
| `npm uninstall <package>`      | Removes a dependency                            |
| `npm run lint`                 | Checks for code quality and style issues        |
| `npm run dev`                  | (Vite projects) Runs dev server faster than CRA |

**Tip:**
Use **npm** or **yarn**, not both in the same project.
Modern setups prefer **pnpm** for performance and disk efficiency.

---

### **30. Environment Variables (.env)**

Environment variables let you **store configuration data** securely outside your code — such as API URLs, secret keys, or modes.

**Create a `.env` file in the root of your project:**

```bash
# Example: .env
VITE_API_URL=https://api.example.com
VITE_APP_NAME=EATSONLINE
```

**Accessing in React:**

```js
console.log(import.meta.env.VITE_API_URL);
```

> ⚠️ In Vite and CRA, **variables must start with `VITE_` (Vite)** or `REACT_APP_` (CRA) to be accessible in the app.

**Why use `.env`:**

- Keeps secrets out of the codebase.
- Makes switching between environments (dev, test, prod) easier.

**Example:**

```
.env.development
.env.production
```

---

### **31. Import/Export and Module Organization**

#### **Types of Exports**

1. **Named Export**

   ```js
   export const sum = (a, b) => a + b;
   export const multiply = (a, b) => a * b;
   ```

   **Import:**

   ```js
   import { sum, multiply } from "./math";
   ```

2. **Default Export**

   ```js
   export default function greet() {
     return "Hello";
   }
   ```

   **Import:**

   ```js
   import greet from "./greet";
   ```

3. **Re-exporting Modules**

   - Used to create **index.js** in each folder for simpler imports:

   ```js
   // components/index.js
   export { default as Navbar } from "./Navbar";
   export { default as Footer } from "./Footer";
   ```

   Then import anywhere:

   ```js
   import { Navbar, Footer } from "@/components";
   ```

**Best Practices:**

- Use **named exports** for multiple utilities or components.
- Use **default export** for single main component per file.
- Keep import paths **clean and relative** (or use path aliases in `vite.config.js` / `jsconfig.json`).

---

### **32. Reusable Components and Utilities**

#### **Reusable Components**

- Components that are **generic**, **configurable**, and can be reused across pages.
- Example: Button, Modal, Card, Loader, FormInput, Toast.

**Example:**

```jsx
function Button({ label, onClick, type = "primary" }) {
  return (
    <button className={`btn btn-${type}`} onClick={onClick}>
      {label}
    </button>
  );
}
```

**Usage:**

```jsx
<Button label="Save" type="primary" onClick={handleSave} />
<Button label="Delete" type="danger" onClick={handleDelete} />
```

#### **Reusable Utilities**

- Helper functions used across the app for consistent logic.
- Keep them in `/src/utils/`.

**Example (utils/formatDate.js):**

```js
export function formatDate(date) {
  return new Date(date).toLocaleDateString("en-GB");
}
```

**Usage:**

```js
import { formatDate } from "@/utils/formatDate";
console.log(formatDate("2025-10-28"));
```

**Why reuse components/utilities?**

- Avoids repetitive code.
- Increases maintainability.
- Enforces consistency in styling and logic.

---

✅ **Summary Table**

| Concept             | Purpose                   | Example                                 |
| ------------------- | ------------------------- | --------------------------------------- |
| Folder structure    | Organize code logically   | `/components`, `/pages`, `/hooks`       |
| npm/yarn scripts    | Automate tasks            | `npm run build`, `npm run dev`          |
| .env                | Manage config safely      | `VITE_API_URL`                          |
| Import/export       | Modularize and reuse code | `import { Navbar } from "@/components"` |
| Reusable components | Consistent UI and logic   | Button, Card, Modal                     |

---
