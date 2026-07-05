# iSee Too — Deployment Guide

This makes iSee Too work for anyone, anywhere, without them needing an
API key. Your OpenAI API key lives safely on Vercel's servers only.

## What's in this folder

- `index.html` — the app itself (unchanged, just now calls your own server)
- `api/analyze.js` — a small serverless function that holds your API key
  and talks to OpenAI (GPT-4o vision) on the app's behalf

---

## Step 1 — Put this on GitHub

1. Go to https://github.com and log in (or create a free account).
2. Click the **+** icon top-right → **New repository**.
3. Name it something like `isee-too`. Keep it **Public** (Vercel's free
   tier works with public repos). Click **Create repository**.
4. On the new repo's page, click **uploading an existing file**.
5. Drag in `index.html` and the whole `api` folder (with `analyze.js`
   inside it) — GitHub will preserve the folder structure.
6. Click **Commit changes**.

Your repo should now show two things at the top level:
```
index.html
api/analyze.js
```

## Step 2 — Deploy to Vercel (free hosting)

1. Go to https://vercel.com and sign up using your GitHub account —
   this is the easiest way, it connects automatically.
2. Click **Add New... → Project**.
3. Find your `isee-too` repository in the list and click **Import**.
4. Vercel will show a settings screen. You don't need to change
   anything — leave the defaults.
5. **Before clicking Deploy**, scroll down to **Environment Variables**.
   This is the important part:
   - Name: `OPENAI_API_KEY`
   - Value: paste your actual OpenAI API key here
     (get one at https://platform.openai.com/api-keys if you don't
     have it yet)
   - Click **Add**.
6. Now click **Deploy**.

Vercel will build and give you a live URL like:

```
https://isee-too.vercel.app
```

That's it. Anyone can open that link on any phone, tablet, or computer,
draw something, and the app will work — no setup on their end at all.

---

## Ongoing costs

Vercel's hosting is free for a project like this. The only cost is
OpenAI API usage — each time a child asks "What did I draw?" it costs
a small fraction of a cent using the GPT-4o model. You can watch usage
and set spending limits at https://platform.openai.com/usage and
https://platform.openai.com/settings/organization/limits.

## Making updates later

Whenever you want to change something in the app:
1. Edit `index.html` in your GitHub repo (or upload a new version).
2. Vercel automatically redeploys within about a minute — no extra
   steps needed.

## If something goes wrong

- If the owl says "My seeing eyes are asleep" for everyone, check that
  the `OPENAI_API_KEY` environment variable is set correctly in
  Vercel's project settings (Settings → Environment Variables).
- If you see errors mentioning "model not found," your OpenAI account
  may need billing set up before GPT-4o vision requests will work —
  check https://platform.openai.com/settings/organization/billing.
- If the site doesn't load at all, check the **Deployments** tab in
  Vercel for a red error message, and send me a screenshot of it.
