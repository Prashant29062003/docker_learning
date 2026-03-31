
### 🐳 Professional Dockerfile Standards

A professional Dockerfile isn't just about making the code run; it’s about **security**, **build speed (caching)**, and **image size**.

Below is a production-ready, refined Dockerfile for a Node.js/Vite project using `pnpm`.

---

## 📄 The Optimized Dockerfile

Dockerfile

```
# 1. BASE IMAGE: Use a specific, lightweight version (Alpine)
FROM node:24-alpine AS base

# 2. DEPENDENCY LAYER: Separate PNPM setup to improve build speed
ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
RUN corepack enable

# 3. DIRECTORY: Set the working directory
WORKDIR /app

# 4. CACHE OPTIMIZATION: Copy only dependency files first
# This prevents re-running 'pnpm install' if only your code changed
COPY package.json pnpm-lock.yaml ./

# 5. INSTALLATION: Install dependencies 
RUN pnpm install --frozen-lockfile

# 6. SOURCE COPY: Copy the rest of the application files
# IMPORTANT: Ensure you have a .dockerignore file to skip local node_modules
COPY . .

# 7. NETWORKING: Document the container's listening port
EXPOSE 5173

# 8. EXECUTION: Start the application
# --host 0.0.0.0 is required for Vite to be accessible outside the container
CMD ["pnpm", "run", "dev", "--host", "0.0.0.0"]
```

---

## 🚫 The Mandatory `.dockerignore`

Without this file, Docker will copy your **local** `node_modules` into the image, which causes the "Module Not Found" or "Architecture Mismatch" errors you saw earlier.

**Create a file named `.dockerignore` in your root folder:**

Plaintext

```
node_modules
dist
.git
.dockerignore
Dockerfile
npm-debug.log
```

---

## 🛠️ Essential CLI Operations

### **Building the Image**

Use a "tag" (`-t`) to name your image so you don't have to remember the ID.

Bash

```
docker build -t vite-app:v1 .
```

### **Running the Container**

|**Flag**|**Meaning**|
|---|---|
|`-p 5173:5173`|**Port Mapping:** Maps `[Your Machine]:[Inside Container]`|
|`-d`|**Detached:** Runs in the background|
|`--name my-vite`|**Naming:** Gives the running instance a readable name|
|`-v /app/node_modules`|**Anonymous Volume:** Protects container node_modules from being overwritten|

**The Professional Run Command:**

Bash

```
docker run -d -p 5173:5173 --name my-site vite-app:v1
```

---

## 💡 Pro-Tips for Production

1. **`--frozen-lockfile`**: In the `pnpm install` step, this ensures that the exact versions in your `pnpm-lock.yaml` are installed. If the lockfile doesn't match `package.json`, the build fails—preventing "it works on my machine" bugs.
    
2. **Multi-Stage Builds**: For a real production site, you would add a second stage using **Nginx** to serve the static files, reducing the image size from ~400MB to ~20MB.
    
3. **Non-Root User**: For high security, add `USER node` before the `CMD` to prevent the container from running with root privileges.