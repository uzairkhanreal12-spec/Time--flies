# Live Tracker (installable PWA)

Growth (green, solid) vs Failure (red, dashed/broken) live tracker.
Adds one point to both graphs every 10 minutes, runs for 15 hours,
and shows an in-app alert banner (+ vibration) every 5 minutes.

Alerts are shown inside the app itself (banner + phone vibration) rather
than as OS push notifications — this avoids permission-prompt and delivery
problems entirely and always works reliably the moment the app is open.

## Files
- `index.html` — the app
- `manifest.json` — makes it installable (name, icons, standalone mode)
- `sw.js` — service worker: caches everything for offline use + shows notifications
- `icons/` — app icons

## 1. Put it on GitHub Pages (free hosting, gives it a real HTTPS URL — required for install + notifications)

1. Go to github.com → **New repository** → name it e.g. `live-tracker` → Public → Create.
2. Click **Add file → Upload files**, drag in all files from this folder
   (keep `icons/` as a subfolder — GitHub preserves the folder structure automatically).
3. Commit the files.
4. Go to **Settings → Pages**.
5. Under "Build and deployment" → Source: **Deploy from a branch**.
6. Branch: `main`, folder: `/ (root)` → **Save**.
7. Wait ~1 minute. Your app will be live at:
   `https://<your-username>.github.io/live-tracker/`

## 2. Install it on Android

1. Open that URL in **Chrome** on your phone.
2. Tap the **⋮** menu → **"Install app"** (or "Add to Home screen").
3. It installs like a real app — own icon, opens full-screen, no address bar.
4. Open it and tap **Start Tracking**. That's it — no permissions needed.

## 3. Offline behaviour

Once installed, the service worker caches everything. Reopen anytime without
internet and it works. Progress is saved in the phone's local storage, so if
you close the app for a while, it catches up automatically based on real
elapsed time when you reopen it.

## Important note on alerts

Alerts only appear while the app is open (banner across the top + a short
vibration) — there's no OS notification permission to manage, so nothing
can silently fail or get blocked. If the app is closed, it simply catches
up the missed points and the countdown when you reopen it; you won't get a
push while it's closed. Getting alerts while fully closed would require a
server-sent push service — a bigger project than a static site.
