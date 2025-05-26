
````markdown
# Vite App Deployment Guide (Local & Google Cloud Run)

This guide outlines how to build and run your Vite application using Docker for both local development and production deployment on Google Cloud Run.

---

## 🧪 Local Development

### 1. Build Development Image
```bash
docker build -f Dockerfile.dev -t vite-dev .
````

### 2. Run Development Container

```bash
docker run -p 5173:5173 vite-dev
```

This exposes the Vite dev server on [http://localhost:5173](http://localhost:5173).

---

## 🚀 Production Build (Google Cloud Run)

### 1. Build Production Docker Image

```bash
docker build -f Dockerfile.prod -t vite-prod .
```

### 2. Run Locally for Testing (Optional)

```bash
docker run -p 8080:80 vite-prod
```

---

## 🌐 Google Cloud Setup

### 1. Set GCP Project

```bash
gcloud config set project tribal-spanner-283108
gcloud auth application-default set-quota-project tribal-spanner-283108
```

### 2. Verify Active Project

```bash
gcloud config get-value project
```

---

## 🔐 Clean Docker Config (if needed)

```bash
rm ~/.docker/config.json
```

---

## 🗃️ Artifact Registry Setup

### 1. Create Artifact Registry (if not already created)

```bash
gcloud artifacts repositories create vite-docker-repo \
  --repository-format=docker \
  --location=asia-south1
```

### 2. List Artifact Registries

```bash
gcloud artifacts repositories list --location=asia-south1
```

---

## 🐳 Push Image to Artifact Registry

### 1. Build with Registry Tag

```bash
docker build -f Dockerfile.prod -t asia-south1-docker.pkg.dev/tribal-spanner-283108/vite-docker-repo/vite-app .
```

### 2. Push to GCP Artifact Registry

```bash
docker push asia-south1-docker.pkg.dev/tribal-spanner-283108/vite-docker-repo/vite-app
```

---

## 🚀 Deploy to Cloud Run

### Deploy the Container

```bash
gcloud run deploy vite-app \
  --image=asia-south1-docker.pkg.dev/tribal-spanner-283108/vite-docker-repo/vite-app \
  --region=asia-south1 \
  --platform=managed \
  --allow-unauthenticated
```

> Note: The container **must listen on port `8080`** for Cloud Run.

---

## 📦 Architecture Overview

```
[Local Dev or Mumbai Cloud Server]
        ↓
    [GCP Account]
        ↓
[Artifact Registry (vite-docker-repo)]
        ↓
     [Cloud Run App: vite-app]
```

---

## 📎 Notes

* Ensure `nginx.conf` uses `listen 8080;` (not `${PORT}`).
* Cloud Run automatically routes requests to container's `EXPOSED` port.
* Vite must be built with `npm run build` before production deployment.

---

## 🛠️ Useful Links

* [Vite Docs](https://vitejs.dev/)
* [Cloud Run Docs](https://cloud.google.com/run/docs)
* [Artifact Registry Docs](https://cloud.google.com/artifact-registry)

---


