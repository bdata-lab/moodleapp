# T10 — Brand Identity in Source

**Branch:** practice/<yourname> or client/bdata
**Date:** 2026-08-17
**Developer:** (Your name here)

---

## Steps Completed

1. [x] Confirmed not on main branch
2. [x] Changed display name → BDATA LMS
3. [x] Changed application id → com.bdata.moodleapp
4. [x] Changed URL scheme → moodlemobile
5. [x] Replaced launcher icon → resources/icon.png + resources/android/icon-foreground.png
6. [x] Replaced splash screen → resources/splash.png
7. [x] Set splash background color → #000000 (black) in config.xml
8. [x] Set StatusBar + NavigationBar color → #000000
9. [ ] Remove / empty demo_sites (still has demo sites — TODO)
10. [ ] git push -u origin <branch> (pending — fix Node version first)

---

## Files Changed

| File | What Changed |
|------|-------------|
| moodle.config.json | app_id, appname, customurlscheme, sites |
| config.xml | Splash background #000000, icon → icon-foreground.png |
| resources/icon.png | Replaced with BDATA logo |
| resources/android/icon-foreground.png | Replaced with BDATA logo |
| resources/splash.png | Replaced with BDATA dark splash |

---

## Screenshots Required (Add Here)

- [ ] home-screen-icon.png — App icon on device home screen
- [ ] splash-screen.png — Splash screen on app launch
- [ ] git-remote-v.txt — Output of: git remote -v

---

## Blockers

- Node v24.18.0 installed — project requires >=v22.17 <23
- Fix: Install nvm-windows → nvm install lts/jod → nvm use lts/jod → npm install

---

## Pass Criteria (Pass Rule)

Another developer could repeat this task from these notes alone.

- [x] Brand files identified and replaced
- [ ] Sideloaded/debug app shows BDATA name, icon, splash, colors
- [ ] Branch exists on bdata-lab/moodleapp
