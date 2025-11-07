### **42. Inline Styles**

- Inline styles in React are written as **JavaScript objects**, not as strings.
- Property names use **camelCase** instead of kebab-case.
- Useful for **dynamic** or **conditional** styles.

Example:

```jsx
function Button({ primary }) {
  const style = {
    backgroundColor: primary ? "blue" : "gray",
    color: "white",
    padding: "10px 15px",
    borderRadius: "8px",
  };
  return <button style={style}>Click Me</button>;
}
```

✅ Pros: Easy for dynamic styling.
❌ Cons: No pseudo-classes (`:hover`) or media queries.

---

### **43. CSS Modules**

- CSS Modules let you write CSS normally but scope it **locally to the component**.
- Class names are automatically **hashed**, so there’s no global conflict.

Example:

```css
/* Button.module.css */
.btn {
  background-color: blue;
  color: white;
  padding: 10px;
}
```

```jsx
import styles from "./Button.module.css";

function Button() {
  return <button className={styles.btn}>Click Me</button>;
}
```

✅ Pros: Scoped styles, no name collisions.
❌ Cons: Slightly more setup for large projects.

---

### **44. Styled-components**

- A **CSS-in-JS** library for styling React components.
- Lets you write actual CSS inside JavaScript using template literals.
- Creates real class names behind the scenes.

Example:

```jsx
import styled from "styled-components";

const Button = styled.button`
  background: ${(props) => (props.primary ? "blue" : "gray")};
  color: white;
  padding: 10px 15px;
  border-radius: 5px;
`;

function App() {
  return <Button primary>Click Me</Button>;
}
```

✅ Pros: Scoped styles, dynamic props, supports themes.
❌ Cons: Larger bundle size than CSS Modules.

---

### **45. Emotion, Tailwind CSS, Sass**

These are **alternative styling approaches** commonly used with React:

#### **🧠 Emotion**

- Similar to styled-components, supports **CSS-in-JS** and **Theming**.
- Example:

  ```jsx
  /** @jsxImportSource @emotion/react */
  import { css } from "@emotion/react";

  const buttonStyle = css`
    background: teal;
    color: white;
    padding: 10px;
  `;

  <button css={buttonStyle}>Click</button>;
  ```

#### **🎯 Tailwind CSS**

- A **utility-first CSS framework** — you style directly with predefined class names.
- Example:

  ```jsx
  <button className="bg-blue-500 text-white px-4 py-2 rounded">Click Me</button>
  ```

✅ Extremely fast development; consistent design system.
❌ Can look cluttered if not managed well.

#### **🎨 Sass (SCSS)**

- A CSS preprocessor with variables, nesting, and mixins.
- Example:

  ```scss
  $main-color: #3498db;

  .button {
    background: $main-color;
    &:hover {
      background: darken($main-color, 10%);
    }
  }
  ```

✅ Powerful CSS features, clean structure.
❌ Needs build setup (already supported in Create React App).

---

### **46. Conditional classNames**

- You often need to toggle styles dynamically based on state or props.
- You can use **ternary operators** or the **classnames** library.

Example (basic ternary):

```jsx
<button className={isActive ? "btn active" : "btn"}>Click</button>
```

Example (using `classnames` library):

```jsx
import clsx from "clsx";

<button className={clsx("btn", { active: isActive, disabled: !isActive })}>
  Click
</button>;
```

✅ Cleaner and scalable for multiple conditions.

---

### **47. Theming in React**

- Theming lets you define **consistent design tokens** (like colors, fonts, spacing) across your app.
- Can be implemented with **Context API** or styling libraries like **styled-components** or **Emotion**.

Example (using styled-components ThemeProvider):

```jsx
import { ThemeProvider } from "styled-components";

const theme = {
  colors: {
    primary: "#007bff",
    secondary: "#6c757d",
  },
};

function App() {
  return (
    <ThemeProvider theme={theme}>
      <Button>Click</Button>
    </ThemeProvider>
  );
}
```

✅ Helps easily switch between **light/dark themes** or brand styles.

---
