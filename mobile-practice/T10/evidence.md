# T10 — Brand Identity in Source

**Branch:** `client/bdata-lms`  
**Date:** 2026-08-21  
**Developer:** BDATA Lab  
**Application ID:** `com.bdata.moodleapp`  
**App Name:** `BDATA LMS`  
**URL Scheme:** `bdatalms`  

---

## 1. Objective

Transform the default Moodle HQ application codebase into a fully branded, private **BDATA LMS** client application:
1. Configure unique application identifier and display name.
2. Update deep-linking URL scheme to `bdatalms://`.
3. Replace all launcher icons (legacy and Android Adaptive icons) with BDATA brand assets.
4. Replace splash screen with custom BDATA dark splash and black background (`#000000`).
5. Update global SCSS brand colors (`$brand-color: #0f6cbf`) to apply BDATA Blue across all buttons, login UI, tabs, and components.
6. Remove/empty default demo sites.

---

## 2. Source Configuration Mapping

| Component | Target File | Configured Value | Description |
|---|---|---|---|
| **App Name** | `config.xml`, `moodle.config.json` | `BDATA LMS` | Display name shown on launcher and headers. |
| **App Identifier** | `config.xml`, `moodle.config.json` | `com.bdata.moodleapp` | Native Android Package ID / iOS Bundle ID. |
| **URL Scheme** | `moodle.config.json`, `package.json` | `bdatalms` | Deep linking scheme for browser SSO and QR auth. |
| **Brand Colors** | `src/theme/globals.variables.scss` | `$brand-color: #0f6cbf` | Primary brand color applied to login buttons and accents. |
| **Demo Sites** | `moodle.config.json` | `{}` (Empty) | Removed Moodle HQ demo sites from app selection. |
| **Splash Background** | `config.xml`, `resources/values/colors.xml` | `#000000` | Black background for dark splash theme. |
| **Launcher Icons** | `config.xml`, `resources/icon.png` | BDATA Logo | Adaptive & standard density launcher icons. |

---

## 3. Files Modified & Replaced

| File | What Changed |
|---|---|
| `moodle.config.json` | Set `app_id: "com.bdata.moodleapp"`, `appname: "BDATA LMS"`, `customurlscheme: "bdatalms"`, `demo_sites: {}`. |
| `config.xml` | Updated widget `id`, `<name>`, `<icon>` densities, `<platform name="android">` adaptive icons, splash colors `#000000`. |
| `src/theme/globals.variables.scss` | Updated `$brand-color: #0f6cbf !default;` (BDATA Blue). |
| `resources/icon.png` | Replaced with BDATA logo. |
| `resources/android/icon-foreground.png` | Replaced with BDATA adaptive foreground. |
| `resources/splash.png` | Replaced with BDATA dark splash image. |
| `src/assets/icon/icon.png`, `favicon.png` | Synchronized with BDATA icon. |
| `src/assets/img/login_logo.png`, `top_logo.png` | Synchronized with BDATA logo. |

---

## 4. Evidence Artifacts

Collected files in this folder (`mobile-practice/T10/`):

| File | Description | Status |
|---|---|---|
| `device-bdata-lms.jpg` | App icon on device launcher screen showing BDATA icon and "BDATA LMS" name. | [x] Collected |
| `device-splash-screen.jpg` | Dark splash screen showing BDATA splash logo on launch. | [x] Collected |
| `device-login-theme.jpg` | In-app login screen showing BDATA Blue primary button and BDATA logo. | [x] Collected |

---

## 5. Pass Criteria

- [x] Confirmed not on `main` branch (working on `client/bdata-lms`).
- [x] Brand display name changed to **BDATA LMS**.
- [x] Package ID changed to **`com.bdata.moodleapp`**.
- [x] Custom URL scheme configured to **`bdatalms`**.
- [x] Launcher icons and Android adaptive icons replaced with BDATA assets.
- [x] Splash screen replaced with BDATA dark splash and `#000000` background.
- [x] SCSS brand color updated to BDATA Blue (`#0f6cbf`).
- [x] Demo sites emptied in `moodle.config.json`.
- [x] Git branch pushed to `origin client/bdata-lms`.

---

## PASS ✅
