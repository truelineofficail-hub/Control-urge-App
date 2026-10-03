# CONTROL

**A calmer mind. A stronger you.**

CONTROL is a private, offline-capable web app (PWA) that helps people get through sexual urges without shame. It teaches one idea:

> An urge is a feeling. A feeling does not have to become an automatic action.

There is no account, no server and no tracking. Everything you enter stays on your own device.

---

## What's inside

| Area | What it does |
|---|---|
| **Urge flow** | Check-in (1-10), a guided pause (1, 2 or 3 minutes) with breathing styles, trigger picker, environment steps tailored to your triggers, a 10-minute reset, and a reassessment. You can leave at any step with no penalty. |
| **Boy / Girl versions** | Triggers, activities, daily tips, Learn articles, gestures and pause wording differ for each, so the advice fits the person. |
| **Reset tab** | Breathing, 10-Minute Reset, Change Environment, Quick Walk, Night plan, Calming gestures. |
| **Calming gestures** | Short, non-sexual actions (2-minute timer), with favorites. |
| **Gradual plan** | Step-down plan: 3x/week, 2x/week, 1x/week, 1x per 2 weeks, 1x/month. Move up or back any time. No streaks. |
| **Learn** | Short articles with a one-question quiz. Mingle mode adds relationship-wellness guides. |
| **Journal** | Private notes, weekly reflection, and a one-tap "add to journal" after a session. |
| **Insights and Progress** | Built only from what you actually logged: common triggers, time of day, mood, sessions, earned badges. No fake numbers. |
| **If-then plans** | "If I feel lonely, then I will..." shown at the right moment in the flow. |
| **Privacy tools** | Optional PIN lock, Discreet mode (neutral "NOTES" name, content hidden when switching apps), and full data reset. |
| **Characters** | Anime-style boy and girl avatars with skin and hair options, or your own picture (stored on device). |

## Design principles

1. Never shame the user. An urge is not a failure.
2. No streaks as the main measure, and no fake statistics.
3. Always give one practical action, not just "stay strong".
4. Reduce cognitive load in strong moments: one instruction at a time.
5. Nothing explicit, ever.
6. The user can always leave, and every button has a defined next state.

---

## Package contents

```
control-pwa/
├── index.html        The whole app (HTML, CSS and JS in one file)
├── manifest.json     PWA metadata, icons and home-screen shortcuts
├── sw.js             Service worker: offline app shell
├── favicon.ico
├── icons/
│   ├── icon-72 ... icon-512.png        Standard icons ("any")
│   ├── icon-maskable-192/512.png       Adaptive icons for Android
│   ├── apple-touch-icon.png            iOS home screen (180x180)
│   ├── favicon-32.png
│   └── source/                         1024px master + rounded preview
└── README.md
```

---

## Run it locally

A service worker needs `http://localhost` or HTTPS, so do not just double-click `index.html`.

```bash
cd control-pwa
python3 -m http.server 8080
# or: npx serve .
```

Open `http://localhost:8080`.

## Deploy

Any static host works. HTTPS is required for install and offline mode.

- **GitHub Pages:** push the folder, then Settings, Pages, deploy from branch.
- **Netlify / Cloudflare Pages / Vercel:** drag the folder in, no build step.

If you host in a sub-folder, nothing needs changing: all paths in the manifest and service worker are relative.

## Install as an app

- **Android (Chrome):** menu, Install app.
- **iPhone (Safari):** Share, Add to Home Screen.
- **Desktop (Chrome/Edge):** install icon in the address bar.

Long-press the installed icon on Android for shortcuts: **I'm having an urge** and **Reset tools**.

## Offline behavior

On the first visit the service worker caches the app shell and icons. After that the app opens and works without a connection, including the full urge flow. Pages are fetched network-first so updates arrive when you're online.

**Updating:** change any file, then bump `CACHE_VERSION` in `sw.js` (for example `v2`). Old caches are deleted automatically and the new version takes over on the next load.

---

## Data and privacy

- All data lives in the browser's `localStorage` under one key, `control`: preferences, journal, sessions, moods, plans, favorites, optional PIN and optional profile pictures.
- Nothing is sent to any server.
- The only third-party request is **Google Fonts** (the Figtree typeface). To remove it, delete the two `fonts.googleapis.com` / `fonts.gstatic.com` lines in `index.html`; the app falls back to the system font. Then the app makes no third-party requests at all.
- **Clearing your browser data erases everything.** There is no backup or sync.
- Profile > Privacy > Reset Personal Data deletes it all inside the app.

### Be honest about the PIN

The PIN lock and Discreet mode are for casual privacy, such as someone glancing at your phone. The PIN is stored unencrypted in `localStorage`, so it does **not** protect against someone who can inspect the browser's storage. Use your device's own lock screen as the real protection.

## Limitations

- **No push notifications.** Reminders are an in-app evening check-in card that appears when you open the app after 8 pm.
- Data is per browser and per device.
- Discreet mode renames the in-app logo and page title. The installed app name and icon come from `manifest.json` and stay "CONTROL". Edit `name`, `short_name` and the icons there if you want a neutral install name.

## Customizing

All content is plain data near the end of the script in `index.html`:

| What | Where to edit |
|---|---|
| Triggers per gender | `TRG()` and the `ENV` object (steps shown for each trigger) |
| Activities | `ACTG` (Boy / Girl x Move / Relax / Focus / Other) |
| Calming gestures | `GS` |
| Daily tips | `TIPG` |
| Articles and quizzes | `ART`, `LEARN()`, `QZ` |
| Gradual plan steps | `STG` |
| Colors | CSS variables in `:root` (`--sage`, `--ink`, ...) |
| Avatars | `boy()` and `girl()` SVG functions, plus `SK` and `HR` color lists |

To regenerate icons, resize `icons/source/control-icon-1024.png` to the sizes listed in `manifest.json`. The maskable icons rely on the artwork staying inside the center 80%, which the master image does.

---

## Important

CONTROL is a self-help tool. It is not medical or mental-health treatment and does not replace professional care. If you feel unsafe, hopeless, or at risk of hurting yourself or someone else, contact your local emergency number or a crisis line in your country right away. If urges feel unmanageable or are affecting your life, consider talking to a doctor or therapist.

## License

Add your own license before sharing publicly. No license file is included.
