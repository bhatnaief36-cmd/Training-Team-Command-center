# TTCC — Training Team Command Center 2026

Single-page dashboard. No build step required.

## Deploy to Vercel

### Option A — Vercel CLI (fastest)
```bash
npm i -g vercel
cd ttcc-vercel
vercel
```
Follow the prompts → your site is live.

### Option B — Vercel Dashboard (drag & drop)
1. Go to https://vercel.com/new
2. Choose **"Deploy from a folder"** or drag the `ttcc-vercel` folder
3. Vercel auto-detects the config → click **Deploy**

### Option C — GitHub (recommended for ongoing updates)
1. Push this folder to a GitHub repo
2. Import the repo at https://vercel.com/new
3. Vercel deploys automatically on every push

## Project Structure
```
ttcc-vercel/
├── public/
│   └── index.html    ← the full dashboard
└── vercel.json       ← routing config
```
