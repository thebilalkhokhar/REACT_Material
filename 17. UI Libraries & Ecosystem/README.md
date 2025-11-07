### **📦 17. UI Libraries & Ecosystem**

#### **105. Material UI (MUI)**

**Material UI (MUI)** is one of the most popular React component libraries based on **Google’s Material Design** principles.
It provides ready-made, customizable, and responsive components.

**Installation:**

```bash
npm install @mui/material @emotion/react @emotion/styled
```

**Example:**

```js
import Button from "@mui/material/Button";

function App() {
  return (
    <Button variant="contained" color="primary">
      Click Me
    </Button>
  );
}
```

✅ Huge set of polished components
✅ Theming support (dark/light mode)
✅ Well-documented and widely used

---

#### **106. Ant Design**

**Ant Design (AntD)** is an enterprise-grade UI framework developed by **Alibaba**, known for its elegant design and powerful form handling.

**Installation:**

```bash
npm install antd
```

**Example:**

```js
import { Button, DatePicker } from "antd";

function App() {
  return (
    <>
      <DatePicker />
      <Button type="primary">Submit</Button>
    </>
  );
}
```

✅ Best for dashboards and admin panels
✅ Great form validation and layout tools
✅ Professional and clean visual style

---

#### **107. Chakra UI**

**Chakra UI** is a **modular, accessible**, and **themeable** React component library that uses **styled-system** for styling props.

**Installation:**

```bash
npm install @chakra-ui/react @emotion/react @emotion/styled framer-motion
```

**Example:**

```js
import { Button, Stack } from "@chakra-ui/react";

function App() {
  return (
    <Stack spacing={4} direction="row">
      <Button colorScheme="teal">Save</Button>
      <Button colorScheme="red">Delete</Button>
    </Stack>
  );
}
```

✅ Dark mode built-in
✅ Responsive props (e.g. `p={{ base: 2, md: 4 }}`)
✅ Great developer experience

---

#### **108. Shadcn/UI**

**Shadcn/UI** is a **modern, minimalist React component library** built with **Tailwind CSS** and **Radix UI primitives**.
It’s designed for **customizable, production-grade UI** with a consistent design system.

**Installation:**

```bash
npx shadcn-ui@latest init
```

**Example:**

```js
import { Button } from "@/components/ui/button";

export default function App() {
  return <Button>Click Me</Button>;
}
```

✅ Built on Tailwind (lightweight + fast)
✅ Great for custom design systems
✅ Perfect for modern apps (e.g., dashboards, SaaS)

---

#### **109. Recharts / Victory for Charts**

**Recharts** and **Victory** are React chart libraries for creating **data visualizations** like bar charts, line charts, and pie charts.

**Recharts Example:**

```js
import { LineChart, Line, XAxis, YAxis, Tooltip } from "recharts";

const data = [
  { name: "Jan", sales: 30 },
  { name: "Feb", sales: 50 },
  { name: "Mar", sales: 70 },
];

function Chart() {
  return (
    <LineChart width={400} height={250} data={data}>
      <Line type="monotone" dataKey="sales" stroke="#8884d8" />
      <XAxis dataKey="name" />
      <YAxis />
      <Tooltip />
    </LineChart>
  );
}
```

✅ Easy to integrate dynamic data
✅ Responsive and customizable
✅ Great for analytics dashboards

---

#### **110. Framer Motion for Animations**

**Framer Motion** is a **powerful animation library** for React used to add smooth transitions, gestures, and effects.

**Installation:**

```bash
npm install framer-motion
```

**Example:**

```js
import { motion } from "framer-motion";

function Box() {
  return (
    <motion.div
      animate={{ x: 100, opacity: 1 }}
      initial={{ opacity: 0 }}
      transition={{ duration: 0.5 }}
      className="w-16 h-16 bg-blue-500"
    />
  );
}
```

✅ Easy-to-use animation API
✅ Supports drag, scroll, and gesture animations
✅ Works perfectly with Tailwind & Chakra

---
