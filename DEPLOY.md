# Deployment Guide

This project is separated into two parts:
1.  **Backend** (Node.js/Express) - Deploys to Render.com
2.  **Frontend** (HTML/CSS/JS) - Deploys to GitHub Pages or Netlify

---

## 1. Backend Deployment (Render.com)

1.  Push your code to GitHub (you have already done this).
2.  Go to [Render Dashboard](https://dashboard.render.com/).
3.  Click **New +** -> **Web Service**.
4.  Connect your GitHub repository (`londonvippanel2`).
5.  Configure the service:
    *   **Name**: `londonvip-backend` (or similar)
    *   **Region**: Frankfurt (or nearest to you)
    *   **Branch**: `main`
    *   **Root Directory**: `backend` (Important! Do not leave empty)
    *   **Runtime**: `Node`
    *   **Build Command**: `npm install`
    *   **Start Command**: `npm start`
6.  **Environment Variables**:
    *   Click "Advanced" or "Environment Variables".
    *   Add `DB_PASSWORD`: Your Database Password (if using local DB, you need a cloud DB like Aiven or Render PostgreSQL. For now, use a cloud database connection string).
    *   Add `JWT_SECRET`: A secure random string.
    *   Add `PORT`: `3000` (Optional, Render sets this automatically).
7.  Click **Create Web Service**.
8.  **Copy the URL**: Once deployed, copy the URL (e.g., `https://londonvip-backend.onrender.com`).

---

## 2. Frontend Deployment (GitHub Pages)

1.  Go to your GitHub repository (`londonvippanel2`).
2.  Go to **Settings** -> **Pages**.
3.  Under **Build and deployment**:
    *   **Source**: `Deploy from a branch`.
    *   **Branch**: `main`.
    *   **Folder**: `/frontend` (Select `/frontend` from the dropdown if available. If not, see "Option B" below).

    *Note: GitHub Pages usually only allows `/` (root) or `/docs`. Since your frontend is in `/frontend`, you might need Option B.*

### Option B: Netlify (Recommended for subfolders)

1.  Go to [Netlify](https://www.netlify.com/).
2.  Click **Add new site** -> **Import from existing project**.
3.  Connect GitHub -> Select `londonvippanel2`.
4.  Configure:
    *   **Base directory**: `frontend`
    *   **Build command**: (Leave empty)
    *   **Publish directory**: `frontend` (or leave default if Base directory is set)
5.  Click **Deploy**.

---

## 3. Connect Frontend to Backend

1.  After deploying the Backend, copy the **Render URL**.
2.  In your local code, open `frontend/assets/js/config.js`.
3.  Update the `API_BASE_URL`:
    ```javascript
    const API_BASE_URL = 'https://londonvip-backend.onrender.com'; // Replace with your actual Render URL
    ```
4.  Commit and push the changes to GitHub.
    ```bash
    git add frontend/assets/js/config.js
    git commit -m "Update API URL for production"
    git push origin main
    ```
5.  Netlify/GitHub Pages will automatically update with the new configuration.
