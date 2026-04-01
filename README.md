# Accommodation Manager — Netlify Deploy Guide

## Project Structure

```
accom-manager/
├── netlify.toml                    ← Netlify build config
├── package.json                    ← Dependencies (Netlify Blobs)
├── public/
│   └── index.html                  ← The full app (served as website)
└── netlify/
    └── functions/
        ├── getData.mjs             ← GET  /api/getData  (load data)
        └── saveData.mjs            ← POST /api/saveData (save data)
```

Data is stored using **Netlify Blobs** — Netlify's built-in key-value store.
No external database needed. No environment variables needed.

---

## How to Deploy (3 steps)

### Step 1 — Push to GitHub

1. Create a new repository on GitHub (can be private)
2. Upload this entire folder to it, or run:
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git remote add origin https://github.com/YOUR_USERNAME/YOUR_REPO.git
   git push -u origin main
   ```

### Step 2 — Connect to Netlify

1. Go to [netlify.com](https://netlify.com) and log in
2. Click **"Add new site"** → **"Import an existing project"**
3. Connect your GitHub account and select the repository
4. Build settings are auto-detected from `netlify.toml`:
   - **Publish directory:** `public`
   - **Functions directory:** `netlify/functions`
5. Click **"Deploy site"**

### Step 3 — Enable Netlify Blobs

Netlify Blobs are enabled **automatically** when your site is deployed.
No extra configuration needed.

---

## That's it!

Your app will be live at `https://YOUR-SITE-NAME.netlify.app`

All data changes (add/edit/delete apartments, rooms, beds) are saved
to Netlify Blobs instantly and persist across all sessions and devices.

---

## How Data Saving Works

- Every change (add/edit/delete) triggers an auto-save after 800ms
- The top-right indicator shows: **Saving…** → **All saved**
- Data is stored as JSON in Netlify Blobs under the key `apartments`
- Use Export / Import to download backups

---

## Local Development (optional)

If you want to test locally before deploying:

```bash
npm install -g netlify-cli
npm install
netlify dev
```

Then open `http://localhost:8888`

> Note: Netlify Blobs requires a real Netlify site to work.
> For local dev, link your site first: `netlify link`
