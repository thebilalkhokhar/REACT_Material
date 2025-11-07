### **🧰 12. Testing**

#### **80. Jest Basics**

**Jest** is a popular testing framework by Facebook used to test JavaScript and React applications.
It provides:

- Test runner
- Assertion library
- Mocking utilities
- Code coverage

**Example:**

```js
// sum.js
export const sum = (a, b) => a + b;

// sum.test.js
import { sum } from "./sum";

test("adds 1 + 2 to equal 3", () => {
  expect(sum(1, 2)).toBe(3);
});
```

✅ Run tests using:

```bash
npm test
```

🧠 Jest automatically looks for files with `.test.js` or `.spec.js` extensions.

---

#### **81. React Testing Library (RTL)**

**React Testing Library (RTL)** is built on top of Jest and focuses on testing **user behavior**, not implementation details.

It provides utilities to render components and simulate user interactions.

**Example:**

```js
import { render, screen, fireEvent } from "@testing-library/react";
import App from "./App";

test("button click updates text", () => {
  render(<App />);
  const button = screen.getByText(/click me/i);
  fireEvent.click(button);
  expect(screen.getByText(/clicked!/i)).toBeInTheDocument();
});
```

✅ Encourages writing tests that resemble **real user interactions**
✅ Works well with Jest

---

#### **82. Snapshot Testing**

Snapshot testing ensures your UI **doesn’t change unexpectedly**.

When you first run a snapshot test, Jest saves a snapshot of the rendered component’s output.
On subsequent runs, it compares new output to the saved snapshot.

**Example:**

```js
import renderer from "react-test-renderer";
import Button from "./Button";

test("Button renders correctly", () => {
  const tree = renderer.create(<Button label="Click" />).toJSON();
  expect(tree).toMatchSnapshot();
});
```

✅ Detects accidental UI changes
⚠️ Update snapshots carefully when intended changes are made:

```bash
npm test -- -u
```

---

#### **83. Mocking API Calls**

You can **mock API calls** in Jest to isolate component behavior from network requests.

**Example:**

```js
global.fetch = jest.fn(() =>
  Promise.resolve({
    json: () => Promise.resolve({ data: "mocked data" }),
  })
);

test("fetches data correctly", async () => {
  const res = await fetch("/api");
  const json = await res.json();
  expect(json.data).toBe("mocked data");
});
```

✅ Ensures tests run quickly and deterministically
✅ Prevents hitting real APIs during testing

---

#### **84. Integration Testing**

Integration testing ensures multiple parts (components, functions, or APIs) **work together correctly**.

Example using RTL:

```js
test("user flow: login -> dashboard", async () => {
  render(<App />);

  fireEvent.change(screen.getByPlaceholderText(/email/i), {
    target: { value: "user@test.com" },
  });
  fireEvent.change(screen.getByPlaceholderText(/password/i), {
    target: { value: "1234" },
  });
  fireEvent.click(screen.getByText(/login/i));

  expect(await screen.findByText(/welcome/i)).toBeInTheDocument();
});
```

✅ Tests the app’s logic end-to-end (within the React layer)
✅ Covers interactions between multiple components

---
