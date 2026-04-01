# CropDoc Frontend - Render Deployment Guide

Follow these steps to deploy your React (Vite) frontend to Render.

## 1. Prerequisites
Ensure your latest code (including the API URL update we just made) is committed and pushed to your GitHub repository (`remixansh/cropdoc`).

## 2. Create a New Static Site
1. Go to your [Render Dashboard](https://dashboard.render.com).
2. Click the **New** button and select **Static Site**.

## 3. Connect Repository
1. Select your `cropdoc` GitHub repository.

## 4. Configuration
Fill in the deployment settings exactly as follows:

- **Name**: `cropdoc-frontend` (or any name you prefer)
- **Branch**: `main`
- **Root Directory**: `frontend`  *(⚠️ Critical: This must be set since the React code is inside the frontend folder)*
- **Build Command**: `npm install && npm run build`
- **Publish Directory**: `dist` *(This is the default output folder for Vite builds)*

> [!NOTE] 
> Because we hardcoded the backend URL directly into `AnalyzingPage.jsx` in the previous step, you do **not** need to set any Environment Variables for the frontend.

## 5. Deploy First, Then Add Rewrite Rules
Click **Create Static Site** at the bottom of the page. Render will now download your code, build it, and publish it!

**CRITICAL STEP (After Creation):**
Since this is a Single Page Application (SPA), direct links (like `/result`) will return a 404 error if someone reloads the page. You must configure a Rewrite rule so the app handles navigation correctly.

1. Once the site is created, look at the left sidebar menu for your new `cropdoc-frontend` site.
2. Click on **Redirects/Rewrites**.
3. Click **Add Rule** and fill it out as follows:
   - **Source**: `/*`
   - **Destination**: `/index.html`
   - **Action**: `Rewrite`
4. Click **Save Changes**.

Once the build finishes, your frontend will be live at the `.onrender.com` URL provided at the top left of the dashboard.
