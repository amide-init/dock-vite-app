Here is a beginner-friendly `README.md` file you can include with your project to help your students understand and follow all the steps to run a **Vite + React** app using **Docker (dev mode, no Nginx)**.

---

````markdown
# 🚀 Vite + React App with Docker (Beginner Friendly)

This project helps you run a React app created using Vite inside Docker — perfect for learning web development without installing Node.js locally.

---

## 📁 Project Setup

Before starting, this project should have these files:

- Vite + React app already created (you can use `npm create vite@latest`)
- A `Dockerfile` (see below)
- A `.dockerignore` file

---

## 🐳 Dockerfile

```Dockerfile
# Use Node.js
FROM node:18

# Set working directory inside container
WORKDIR /app

# Copy all files to container
COPY . .

# Install project dependencies
RUN npm install

# Open port for Vite dev server
EXPOSE 5173

# Start Vite development server
CMD ["npm", "run", "dev", "--", "--host"]
````

---

## 📦 .dockerignore

```txt
node_modules
dist
Dockerfile
.dockerignore
```

---

## 🛠️ How to Build the Docker Image

In the terminal, run this:

```bash
docker build -t vite-student .
```

This tells Docker to:

* Read the Dockerfile
* Prepare everything
* Create an image named `vite-student`

---

## ▶️ How to Run the App

Run this command to start the app:

```bash
docker run -p 5173:5173 -v $PWD:/app vite-student
```

### ✅ What this does:

* `-p 5173:5173`: Makes the app visible at `http://localhost:5173`
* `-v $PWD:/app`: Syncs your project folder with the container for live changes

---

## 🌐 Open Your Browser

Go to:

```
http://localhost:5173
```

You should see your React app running!

---

## 📚 What You'll Learn

* How Docker can run your app without installing Node.js on your computer
* How port `5173` allows you to access the app in a browser
* How volume `-v` helps you develop live without restarting

---

## 🧠 Tips for Students

| Concept  | What It Means                                |
| -------- | -------------------------------------------- |
| `build`  | Make a Docker image                          |
| `run`    | Start the container (like a mini computer)   |
| `EXPOSE` | Open a port in the container                 |
| `CMD`    | What command should run inside the container |

---

## 📌 Bonus

If `npm run dev` doesn't auto-reload changes, press `Ctrl + C` to stop the container and re-run it. Or edit your Vite config to use polling.

---

Happy coding! 😄

```

---

Let me know if you want this in PDF or want a **diagram showing host ↔ container port mapping**!
```
