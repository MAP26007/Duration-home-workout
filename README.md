# Performance DURATION

Installable home-workout PWA (no build step, no dependencies).

## Run
Open `index.html` through any static server (service workers need http/https), e.g. `python3 -m http.server`.

## Deploy on GitHub Pages
Push these files to a repo > Settings > Pages > Deploy from branch `main` / root.

## Files
`index.html` (app) · `manifest.json` · `sw.js` · `logo.png`

## Live users: important
This version stores accounts, chat, scores and group sessions in the browser (`localStorage`), so "live" works across tabs/windows on one device. To make users on **different devices** see each other, replace the `DB` object in `index.html` with Firebase Firestore or Supabase Realtime (same keys: `users`, `chat`, `group`, `feed`, `plans`). Passwords are only hashed-lite for demo purposes; use real auth (Firebase Auth/Supabase Auth) in production.

## Editing the app (owner only)
The public app has no admin features. Use the separate `admin.html` (keep it outside this repo, never upload it). Unlock with your owner password, edit, press **Save**, then **Sync to users**. Sync commits `config.json` (and any uploaded media into `media/`) to this repo via the GitHub API; GitHub Pages republishes in 1-2 minutes. Set it up once in the Sync tab with a fine-grained token limited to this repo (Contents: Read and write). The token is stored only on your device.

## Going live (shared scoreboard, chat, feed, group workouts)
1. Create a free Firebase project. Add a Realtime Database (locked mode) and enable Authentication > Email/Password.
2. In `admin.html` > Live, paste the database URL and Web API key, publish these rules: `{"rules":{".read":"auth!=null",".write":"auth!=null"}}`, then Sync to users.
3. Every account created in the app is then a real shared account.
