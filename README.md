# Day 1 — React App S3 Pipeline

A React app with a fully automated CI/CD pipeline that builds and deploys to AWS S3 static website hosting on every push to `master`.

---

## Architecture

![Architecture Diagram](Architecture%20Diagram.png)

The flow:
1. Developer pushes code to GitHub
2. GitHub Actions triggers the workflow
3. React app is built using Vite
4. AWS credentials are configured securely via GitHub Secrets
5. S3 bucket is created (if it doesn't exist), configured for public static hosting
6. Built `dist/` files are synced to the S3 bucket
7. Site is live via the S3 static website URL

---

## Tech Stack

- React + Vite
- GitHub Actions (CI/CD)
- AWS S3 (Static Website Hosting)
- AWS CLI

---

## Pipeline Steps

| Step | Description |
|------|-------------|
| Checkout Code | Pulls the latest code from the repo |
| Setup Node | Installs Node.js v20 |
| Install Dependencies | Runs `npm install` |
| Build React App | Runs `npm run build` to generate `dist/` |
| Configure AWS Credentials | Authenticates using GitHub Secrets |
| Create S3 Bucket | Creates the bucket if it doesn't already exist |
| Disable Block Public Access | Allows public access on the bucket |
| Set Bucket Policy | Grants public read access to all objects |
| Enable Static Website Hosting | Configures `index.html` as the entry point |
| Upload to S3 | Syncs `dist/` to the S3 bucket |
| Print Website URL | Outputs the live site URL in the workflow logs |

---

## Setup

### 1. Add GitHub Secrets

Go to your repo → Settings → Secrets and variables → Actions, and add:

| Secret | Description |
|--------|-------------|
| `AWS_ACCESS_KEY_ID` | Your AWS access key |
| `AWS_SECRET_ACCESS_KEY` | Your AWS secret key |

> Region is hardcoded to `us-east-1` in the workflow — no need to add it as a secret.

### 2. Push to master

```bash
git push origin master
```

The pipeline runs automatically and your site will be live at:

```
http://day-1-react-app-s3-pipeline.s3-website-us-east-1.amazonaws.com
```

---

## Local Development

```bash
npm install
npm run dev
```
