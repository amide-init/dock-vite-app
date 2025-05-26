---

````markdown
# 🔐 Setup Google Cloud Service Account Key for GitHub Actions

This guide will help you create a service account and generate a key to use in GitHub Actions for deploying your Vite app to Cloud Run.

---

## 📌 Step 1: Create a Service Account

```bash
gcloud iam service-accounts create vite-deployer \
  --display-name "Vite Deployer"
````

This creates a service account like:

```
vite-deployer@<your-project-id>.iam.gserviceaccount.com
```

For example:

```
vite-deployer@tribal-spanner-283108.iam.gserviceaccount.com
```

---

## 🔑 Step 2: Assign Required Roles

```bash
gcloud projects add-iam-policy-binding tribal-spanner-283108 \
  --member="serviceAccount:vite-deployer@tribal-spanner-283108.iam.gserviceaccount.com" \
  --role="roles/run.admin"

gcloud projects add-iam-policy-binding tribal-spanner-283108 \
  --member="serviceAccount:vite-deployer@tribal-spanner-283108.iam.gserviceaccount.com" \
  --role="roles/artifactregistry.writer"

gcloud projects add-iam-policy-binding tribal-spanner-283108 \
  --member="serviceAccount:vite-deployer@tribal-spanner-283108.iam.gserviceaccount.com" \
  --role="roles/iam.serviceAccountUser"
```

---

## 🗝️ Step 3: Generate the JSON Key

```bash
gcloud iam service-accounts keys create key.json \
  --iam-account=vite-deployer@tribal-spanner-283108.iam.gserviceaccount.com
```

This will generate a `key.json` file in your current directory.

> ⚠️ **Keep this file safe! Never share it or commit it to GitHub.**

---

## 🔐 Step 4: Add Key to GitHub Secrets

1. Open your GitHub repository.
2. Go to **Settings > Secrets and variables > Actions**.
3. Click **New repository secret**.
4. Name it: `GCP_SA_KEY`
5. Paste the full contents of `key.json` into the value field.
6. Click **Add secret**.

---

## ✅ You're Done!

Your GitHub Actions workflow can now use this secret to:

* Authenticate with Google Cloud
* Push Docker images to Artifact Registry
* Deploy your app to Cloud Run

---

