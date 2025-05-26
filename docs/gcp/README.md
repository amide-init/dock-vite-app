### ✅ `README.md` – Google Cloud Login and Project Setup via Terminal

````markdown
# ☁️ Google Cloud Setup via Terminal (gcloud CLI)

This guide explains how to log in to Google Cloud, view accounts, manage projects, and set a default project using the terminal.

---

## ✅ Prerequisites

- Google Cloud SDK installed  
  👉 [Install instructions](https://cloud.google.com/sdk/docs/install)

- Run in your terminal to check:
  ```bash
  gcloud version
````

---

## 🔐 1. Login to Google Cloud

Start the login process:

```bash
gcloud auth login
```

* This will open your browser
* Choose the Google account you want to use
* Grant access when prompted

---

## 👤 2. View All Logged-In Accounts

```bash
gcloud auth list
```

Output will look like:

```
Credentialed Accounts:
 - old-email@gmail.com
 - new-email@gmail.com (active)
```

---

## 🔄 3. Switch to a Different Account (if needed)

```bash
gcloud config set account your-email@gmail.com
```

---

## 📁 4. View All GCP Projects Linked to Your Account

```bash
gcloud projects list
```

Output example:

```
PROJECT_ID              NAME                 PROJECT_NUMBER
my-demo-project         Demo Project         111111111111
vite-prod-app           Vite Prod App        222222222222
```

---

## 📌 5. Set Active Project

Choose the project you want to work with:

```bash
gcloud config set project your-project-id
```

Example:

```bash
gcloud config set project vite-prod-app
```

---

## ✅ 6. Confirm Active Configuration

```bash
gcloud config list
```

Output:

```yaml
[core]
account = your-email@gmail.com
project = vite-prod-app
```

---

## 🧼 7. Optional: Revoke Old Account (if needed)

```bash
gcloud auth revoke old-email@gmail.com
```

---

## 🎉 You're Ready!

Now you can run any `gcloud` command, and it will use the selected account and project.

Examples:

```bash
gcloud run deploy
gcloud builds submit
gcloud artifacts repositories create ...
```

---

