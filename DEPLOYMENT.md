# 📐 Ingenio Studio Brain — Cloud Deployment Guide

Deploy your premium Studio Brain helper application to the cloud for **100% Free** with **permanently online persistence**, requiring **zero credit cards** for sign-up!

---

## 🛠️ Infrastructure Stack (100% Free & Zero-Card)
We utilize two industry-leading developer tools that offer generous free tiers with no credit card registration:
1. **Vercel Hobby Tier**: For hosting the Node.js Express serverless API and premium front-end web dashboard.
2. **Upstash Redis Free Tier**: For a fast, reliable, permanently free serverless cloud JSON database (10,000 requests per day limit, which is more than enough for active studio tracking).

---

## 🚀 Step 1: Create Your Upstash Redis Database (Free)
1. Go to [Upstash Console](https://console.upstash.com/) and sign up with **Google** or **GitHub** (No credit card needed).
2. Click **Create Database**.
3. Fill in the following details:
   - **Name**: `studio-brain-db`
   - **Type**: `Global` or regional near your studio location.
4. Once created, scroll down to the **REST API** section of your database details page.
5. Click on the **.env** tab to copy the environment variable keys:
   - `KV_REST_API_URL` (or `UPSTASH_REDIS_REST_URL`)
   - `KV_REST_API_TOKEN` (or `UPSTASH_REDIS_REST_TOKEN`)
6. Save these values safely. You will input them in Vercel. (Both naming styles are supported automatically by our standardized backend!).

---

## 📦 Step 2: Push Your Code to GitHub
1. Create a new **Private** or **Public** repository on [GitHub](https://github.com/).
2. Push your studio project folder to the repository:
   ```bash
   git init
   git add .
   git commit -m "Initialize Ingenio Studio Brain"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPOSITORY.git
   git push -u origin main
   ```

---

## ☁️ Step 3: Deploy to Vercel (Free)
1. Go to [Vercel](https://vercel.com/) and sign up with your **GitHub** account.
2. Click **Add New** > **Project**.
3. Import your studio repository from your GitHub list.
4. In the **Configure Project** stage:
   - Expand the **Environment Variables** section.
   - Add the following environment variable keys with the values from Step 1 (either naming convention works perfectly!):
     - `KV_REST_API_URL` *(or `UPSTASH_REDIS_REST_URL`)* ➡️ *(Paste value from Upstash REST API)*
     - `KV_REST_API_TOKEN` *(or `UPSTASH_REDIS_REST_TOKEN`)* ➡️ *(Paste token from Upstash REST API)*
5. Click **Deploy**. Vercel will build and serve your studio dashboard in under a minute!
6. Once deployed, copy your production domain URL (e.g., `https://your-app.vercel.app`).

---

## 🤖 Step 4: Link Your Telegram Bot Webhook
1. Access your deployed Vercel domain URL in your browser.
2. Navigate to the **Telegram Hub** settings pane.
3. Paste your **Telegram Bot Token** and **Gemini AI API Key** into their fields, then click **Save Configuration**.
4. Click the purple button: **⚡ Register Cloud Webhook**.
5. You will see a success message indicating your Telegram bot is now officially linked to Vercel's serverless endpoint.
6. From this point on, **any team member voice note or text sent to your Telegram bot will instantly wake up the serverless function, process the EOD logs, and save them straight to your Upstash Cloud Database!**

---

> [!NOTE]
> **Vercel Serverless Function Lifespan**
> Since Vercel runs on stateless serverless functions, traditional active polling loops and timer daemons inside Express would crash or freeze. Our updated architecture relies entirely on stateless webhooks (handled instantly by `/api/telegram-webhook`) and pre-configured Vercel Cron routes (`/api/cron-reminders` at 9:00 PM and `/api/cron-morning` at 9:30 AM), ensuring 100% cloud reliability for free.

> [!TIP]
> **Automatic Local-to-Cloud Migration**
> When your Vercel app boots up for the first time, it checks your Upstash database. If the database is completely empty, it automatically detects your existing `db.json` database file from the code deployment and uploads it to the cloud. This makes migrating your local history to the cloud completely transparent and seamless!
