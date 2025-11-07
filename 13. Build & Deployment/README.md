### **🚀 13. Build & Deployment**

#### **85. Production Build (`npm run build`)**

When your React app is ready for deployment, you create a **production build** to optimize performance.

**Command:**

```bash
npm run build
```

This generates a `build/` folder containing:

- Minified JavaScript and CSS files
- Optimized images
- Static HTML (`index.html`)

✅ Smaller file sizes
✅ Faster load times
✅ Tree-shaking removes unused code

You then deploy the `build/` folder to a hosting service.

---

#### **86. Environment Configurations for Prod/Dev**

Environment variables let you switch between **development** and **production** setups easily.
These are stored in `.env` files.

**Examples:**

```
.env.development
REACT_APP_API_URL=http://localhost:4000

.env.production
REACT_APP_API_URL=https://api.myapp.com
```

Usage in React:

```js
const apiUrl = process.env.REACT_APP_API_URL;
```

⚠️ All React environment variables must start with `REACT_APP_`
✅ Helps manage API URLs, keys, or feature flags separately for dev/prod.

---

#### **87. Hosting (Vercel, Netlify, Render, etc.)**

Once you have a production build, you can host your React app on cloud platforms:

**Common Hosting Options:**

- **Vercel** – seamless deployment from GitHub
- **Netlify** – easy drag & drop or CI/CD setup
- **Render** – great for monorepos (frontend + backend)
- **GitHub Pages** – good for static personal projects
- **Firebase Hosting** – great for full-stack apps

**Vercel Example:**

- Connect your GitHub repo
- Vercel automatically detects React
- Builds & deploys with every push

✅ Instant rollbacks
✅ Custom domains
✅ Free SSL certificates

---

#### **88. Using Docker with React**

Docker helps you **containerize** your React app so it runs identically everywhere (local, staging, production).

**Example Dockerfile:**

```dockerfile
# Step 1: Build React app
FROM node:18 AS build
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build

# Step 2: Serve app with Nginx
FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

✅ Consistent environment
✅ Easy deployment on any server or cloud

Run commands:

```bash
docker build -t react-app .
docker run -p 3000:80 react-app
```

---

#### **89. CI/CD Basics**

**Continuous Integration (CI)** and **Continuous Deployment (CD)** automate building, testing, and deploying your app whenever you push code.

**Common Tools:**

- GitHub Actions
- GitLab CI
- CircleCI
- Jenkins

**Example GitHub Actions workflow:**

```yaml
name: Deploy React App

on:
  push:
    branches: [main]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install and Build
        run: |
          npm install
          npm run build
      - name: Deploy to Vercel
        uses: amondnet/vercel-action@v20
        with:
          vercel-token: ${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: ${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: ${{ secrets.VERCEL_PROJECT_ID }}
```

✅ Ensures your app is automatically tested & deployed
✅ Minimizes human error and speeds up development

---
