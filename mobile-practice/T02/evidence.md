# T02 — Map Current Branding Files (Source of Truth)

**Date:** 2026-08-17
**Branch:** client/bdata-lms
**Tag:** v5.2.1

---

## Branding File Table

| Purpose | File you found |
|---------|---------------|
| App name, app id, site URL, demo sites, URL scheme | moodle.config.json |
| SCSS/CSS variables (primary colour, login) | src/theme/globals.variables.scss |
| Icons / splash pipeline | resources/icon.png, resources/android/icon-foreground.png, resources/splash.png |
| Android applicationId | config.xml (widget id) — currently: com.moodle.moodlemobile — BDATA: com.bdata.moodleapp (moodle.config.json) |
| iOS bundle id | config.xml (ios-CFBundleVersion) — same widget id |
| npm scripts for browser / Android / iOS / release | package.json scripts section |

---

## Key Values Found

### moodle.config.json
- app_id: com.bdata.moodleapp
- appname: BDATA LMS
- customurlscheme: moodlemobile
- sites[0].url: https://moodle.bdata.com.mm
- demo_sites: student + teacher (moodledemo.net) — to be removed
- default_lang: en

### src/theme/globals.variables.scss
- brand-color: #f98012 (orange)
- primary blue: #0f6cbf
- green: #357a32
- red: #ca3120

### config.xml
- widget id: com.moodle.moodlemobile (upstream default — override in moodle.config.json for branded build)
- android-versionCode: 52100
- version: 5.2.1

### resources/
- resources/icon.png                     — main app icon (replaced with BDATA logo)
- resources/android/icon-foreground.png  — Android adaptive icon fg (replaced)
- resources/splash.png                   — splash screen (replaced with BDATA dark)
- resources/android/android-splash.xml   — original vector splash (replaced by PNG in config.xml)

### package.json scripts
| Script | Command |
|--------|---------|
| start:win | ionic serve --no-open (Windows, no SSL) |
| start | ionic serve --ssl (Linux/Mac) |
| dev:android | concurrently npm run dev:android:app + cordova |
| dev:ios | ionic cordova run ios |
| build | ionic build --configuration=development |
| build:prod | NODE_ENV=production ionic build --prod |

---

## Notes
- config.xml widget id is upstream default; BDATA app_id is set in moodle.config.json
- Do NOT commit keystores or production google-services.json / GoogleService-Info.plist
- Upstream Firebase example files exist in root — not BDATA keys

---

## PASS ✅
