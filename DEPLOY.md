# Getting Lift onto your iPhone

This folder (`lift-live`) is a complete, installable web app (PWA). Host it on a URL,
then Add to Home Screen. It works offline once installed — perfect for gym dead-spots.

## What's in here
- `index.html` — the app
- `manifest.webmanifest` — app name, icon, standalone display
- `sw.js` — service worker (offline caching)
- `icons/` — app icons
- `render.yaml` — optional Render config

---

## Step 1 — Put these files in a Git repo

Render deploys static sites from a Git repository. From this folder:

```bash
cd lift-live
git init
git add .
git commit -m "Lift PWA v1"
```

Then create an empty repo on GitHub (github.com/new, e.g. `lift-app`) and push:

```bash
git remote add origin https://github.com/<your-username>/lift-app.git
git branch -M main
git push -u origin main
```

## Step 2 — Deploy on Render

1. Go to **dashboard.render.com** → **New +** → **Static Site**.
2. Connect the GitHub repo you just pushed.
3. Settings:
   - **Build Command:** *(leave blank)*
   - **Publish Directory:** `.`
4. Click **Create Static Site**. In ~1 minute you get a URL like
   `https://lift-app.onrender.com`.

> The included `render.yaml` sets these automatically if Render picks it up.

## Step 3 — Install on your iPhone

1. Open the Render URL in **Safari** (must be Safari, not Chrome, for Add to Home Screen).
2. Tap the **Share** button (square with an up-arrow).
3. Scroll down → **Add to Home Screen** → **Add**.
4. Launch it from the new **Lift** icon. It opens fullscreen, no Safari bars, with
   the amber dumbbell icon — just like a native app.

Your data (workouts, weigh-ins, history) is stored on the phone in that installed app.

---

## Updating the app later
Change files → `git commit` → `git push`. Render redeploys automatically.
Bump the `CACHE` version in `sw.js` (e.g. `lift-v2`) so phones pull the new version.

## Next upgrade: Supabase sync (optional)
Right now data lives only on the installed device. To sync across phones/devices,
wire the app to your Supabase project (a `weigh_ins` and `sessions` table + anonymous
or email auth). Ask and I'll build the sync layer.
