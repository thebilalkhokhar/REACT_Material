### **🔔 16. Real-Time & Advanced Integrations**

#### **100. WebSockets / Socket.io**

**WebSockets** enable real-time, bidirectional communication between the client and server — perfect for chat apps, notifications, and live dashboards.
**Socket.io** is a library built on top of WebSockets that handles reconnections and event-based messaging more easily.

**Example (Client side):**

```js
import { io } from "socket.io-client";

const socket = io("http://localhost:4000");

socket.on("connect", () => console.log("Connected to server"));
socket.on("message", (msg) => console.log(msg));

// Send data
socket.emit("sendMessage", "Hello Server!");
```

✅ Real-time updates
✅ Ideal for chat, live feeds, collaborative tools

---

#### **101. Server-Sent Events (SSE)**

**SSE** is another real-time communication method where the **server pushes continuous updates** to the client over HTTP (unidirectional).

**Example:**

```js
useEffect(() => {
  const eventSource = new EventSource("http://localhost:4000/events");
  eventSource.onmessage = (e) => console.log(e.data);
  return () => eventSource.close();
}, []);
```

✅ Simpler than WebSockets for one-way updates (e.g., stock prices, notifications)
⚠️ Only server → client, not bidirectional

---

#### **102. Firebase Integration**

**Firebase** is a Google platform offering tools like real-time databases, authentication, storage, and hosting.

**Common integrations:**

- Firebase Authentication (Google, Email/Password)
- Firestore Database (real-time)
- Firebase Storage (file uploads)
- Firebase Hosting (deploy React apps)

**Example:**

```js
import { initializeApp } from "firebase/app";
import { getFirestore, collection, getDocs } from "firebase/firestore";

const firebaseConfig = { apiKey: "XYZ", projectId: "myapp" };
const app = initializeApp(firebaseConfig);
const db = getFirestore(app);

const querySnapshot = await getDocs(collection(db, "users"));
querySnapshot.forEach((doc) => console.log(doc.data()));
```

✅ Real-time database sync
✅ Built-in auth and hosting

---

#### **103. GraphQL (Apollo / URQL)**

**GraphQL** is a query language that allows clients to **request exactly the data they need** from an API — no underfetching or overfetching.

**Apollo Client** and **URQL** are popular React libraries for GraphQL integration.

**Example (Apollo Client):**

```js
import { useQuery, gql } from "@apollo/client";

const GET_USERS = gql`
  query {
    users {
      id
      name
    }
  }
`;

function App() {
  const { loading, error, data } = useQuery(GET_USERS);
  if (loading) return <p>Loading...</p>;
  if (error) return <p>Error :(</p>;
  return data.users.map((u) => <p key={u.id}>{u.name}</p>);
}
```

✅ Declarative data fetching
✅ Strongly typed schema
✅ Efficient and modern alternative to REST

---

#### **104. Next.js (SSR / SSG / ISR Concepts)**

**Next.js** is a React framework that adds:

- **Server-Side Rendering (SSR)** → Fetch data on every request
- **Static Site Generation (SSG)** → Pre-render at build time
- **Incremental Static Regeneration (ISR)** → Regenerate pages periodically

**Rendering Modes:**

| Mode    | Description                          | Function               |
| ------- | ------------------------------------ | ---------------------- |
| **CSR** | Client-Side Rendering                | Default React behavior |
| **SSR** | Server-Side Rendering                | `getServerSideProps()` |
| **SSG** | Static Site Generation               | `getStaticProps()`     |
| **ISR** | Regenerate static pages periodically | `revalidate` property  |

**Example (SSG with ISR):**

```js
export async function getStaticProps() {
  const res = await fetch("https://api.example.com/posts");
  const posts = await res.json();

  return {
    props: { posts },
    revalidate: 10, // regenerate every 10 seconds
  };
}
```

✅ SEO-friendly
✅ Faster load times
✅ Hybrid rendering (SSR + SSG)

---
