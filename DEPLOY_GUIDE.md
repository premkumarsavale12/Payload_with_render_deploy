# Deployment Guide for Railway

This guide will walk you through deploying your Payload CMS + Next.js application to [Railway](https://railway.app/).

## Prerequisites
- A GitHub account with this project repository.
- A Railway account (Login with GitHub recommended).

## Step 1: Create a Project on Railway
1. Go to your [Railway Dashboard](https://railway.app/dashboard).
2. Click **+ New Project**.
3. Select **Deploy from GitHub repo**.
4. Select your **railway-project** repository.
5. Click **Deploy Now**. 
   > **Note:** The initial deployment might fail because environment variables are missing. This is normal.

## Step 2: Add a PostgreSQL Database
1. In your project view on Railway, click the **+ Create** button (or right-click almost anywhere) to add a service.
2. Select **Database** -> **PostgreSQL**.
3. Wait for the database service to initialize.

## Step 3: Configure Environment Variables
1. Click on your **railway-project** service (the application, not the database).
2. Go to the **Variables** tab.
3. You need to add the following variables:

| Variable Name | Value Description |
| :--- | :--- |
| `DATABASE_URL` | **Auto-filled**. Railway creates a `DATABASE_URL` variable for you if you restart the service, OR you can manually copy it from the PostgreSQL service > **Connect** tab. |
| `PAYLOAD_SECRET` | A long random string (e.g., generated via `openssl rand -hex 32` or a password generator). |
| `NEXT_PUBLIC_SERVER_URL` | The public URL of your app. Finds this in the **Settings** tab under **Networking** (e.g., `https://web-production-xxxx.up.railway.app`). |
| `CRON_SECRET` | Another random string for cron job authentication. |

> **Tip:** You can reference the `DATABASE_URL` from the Postgres service by typing `${{PostgreSQL.DATABASE_URL}}` as the value if they are in the same project.

## Step 4: Finalize Deployment
1. Once variables are set, Railway should automatically redeploy.
2. If it doesn't, go to the **Deployments** tab and click **Redeploy**.
3. Wait for the build to complete.
4. Click the generated URL to view your live site!

## Troubleshooting
- **Build Fails?** Check the **Build Logs** for errors.
- **App Crashes?** Check the **Deploy Logs**.
- **Database Connection Error?** Ensure `DATABASE_URL` is correct and the database service is running.

---
**Done!** Your Payload CMS app is now hosted on Railway.
