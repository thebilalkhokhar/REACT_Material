### **56. Controlled Forms**

- In a **controlled form**, React controls the form data through **state** (`useState`).
- Every keystroke updates the state, and the UI always reflects the current value.

Example:

```jsx
function LoginForm() {
  const [email, setEmail] = useState("");
  const [password, setPassword] = useState("");

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(email, password);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input
        value={email}
        onChange={(e) => setEmail(e.target.value)}
        placeholder="Email"
      />
      <input
        value={password}
        onChange={(e) => setPassword(e.target.value)}
        type="password"
        placeholder="Password"
      />
      <button type="submit">Login</button>
    </form>
  );
}
```

✅ Pros: Full control of form data, real-time validation possible.
❌ Cons: More re-renders, verbose for large forms.

---

### **57. Uncontrolled Forms**

- The input values are handled directly by the **DOM**, not React state.
- You use **refs** to access values when needed.

Example:

```jsx
function UncontrolledForm() {
  const emailRef = useRef();
  const passwordRef = useRef();

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(emailRef.current.value, passwordRef.current.value);
  };

  return (
    <form onSubmit={handleSubmit}>
      <input ref={emailRef} placeholder="Email" />
      <input ref={passwordRef} type="password" placeholder="Password" />
      <button type="submit">Login</button>
    </form>
  );
}
```

✅ Pros: Fewer re-renders, simpler for small forms.
❌ Cons: Harder to validate or show live errors.

---

### **58. Formik & Yup Validation**

- **Formik** simplifies managing form state, validation, and submission.
- **Yup** is a schema validation library used with Formik for clean validation rules.

Install:

```bash
npm install formik yup
```

Example:

```jsx
import { useFormik } from "formik";
import * as Yup from "yup";

function SignupForm() {
  const formik = useFormik({
    initialValues: { name: "", email: "" },
    validationSchema: Yup.object({
      name: Yup.string().required("Name is required"),
      email: Yup.string().email("Invalid email").required("Email is required"),
    }),
    onSubmit: (values) => console.log(values),
  });

  return (
    <form onSubmit={formik.handleSubmit}>
      <input
        name="name"
        value={formik.values.name}
        onChange={formik.handleChange}
      />
      {formik.errors.name && <p>{formik.errors.name}</p>}

      <input
        name="email"
        value={formik.values.email}
        onChange={formik.handleChange}
      />
      {formik.errors.email && <p>{formik.errors.email}</p>}

      <button type="submit">Submit</button>
    </form>
  );
}
```

✅ Pros: Reduces boilerplate, integrates well with Yup.
✅ Perfect for large, complex forms.

---

### **59. React Hook Form**

- A **lightweight alternative** to Formik, using uncontrolled components and refs for performance.
- Handles form state, validation, and submission easily.

Install:

```bash
npm install react-hook-form
```

Example:

```jsx
import { useForm } from "react-hook-form";

function ContactForm() {
  const {
    register,
    handleSubmit,
    formState: { errors },
  } = useForm();

  const onSubmit = (data) => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)}>
      <input {...register("email", { required: "Email required" })} />
      {errors.email && <p>{errors.email.message}</p>}

      <input {...register("message", { minLength: 5 })} />
      <button type="submit">Send</button>
    </form>
  );
}
```

✅ Pros: Very fast, minimal re-renders, easy validation.
✅ Great for performance-sensitive apps.

---

### **60. Custom Input Components**

- Reusable input fields that encapsulate behavior, styling, and validation.
- Commonly used with Formik or React Hook Form.

Example:

```jsx
function TextInput({ label, name, register, errors, ...rest }) {
  return (
    <div>
      <label>{label}</label>
      <input {...register(name)} {...rest} />
      {errors[name] && <p>{errors[name].message}</p>}
    </div>
  );
}

// Usage with React Hook Form
<TextInput
  label="Email"
  name="email"
  register={register}
  errors={errors}
  placeholder="Enter your email"
/>;
```

✅ Pros: Clean code, reusable across forms, consistent UX.
✅ Encourages component-based design.

---
