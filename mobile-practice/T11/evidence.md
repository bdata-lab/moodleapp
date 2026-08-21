# T11 — Staging Site URL Configuration & Pre-fill

**Date:** 2026-08-21  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**LMS Staging URL:** `https://moodle.bdata.com.mm`  
**Config File:** `moodle.config.json`  

---

## 1. Objective

Configure the target LMS server URL directly within the mobile application source configuration (`moodle.config.json`):
1. Hardcode/pre-fill the staging URL (`https://moodle.bdata.com.mm`) so learners are directly connected to BDATA LMS without having to manually type the site URL.
2. Define the primary site entry in the `sites` array.
3. Rebuild the web assets and synchronize with the native Android platform.
4. Verify on device that the app launches directly to the BDATA LMS authentication screen.

---

## 2. Configuration Settings (`moodle.config.json`)

```json
{
    "app_id": "com.bdata.moodleapp",
    "appname": "BDATA LMS",
    "versioncode": 52100,
    "versionname": "5.2.1",
    "customurlscheme": "bdatalms",
    "sites": [
        {
            "id": "bdata",
            "name": "BDATA LMS",
            "url": "https://moodle.bdata.com.mm"
        }
    ],
    "privacypolicy": "https://moodle.bdata.com.mm",
    "notificoncolor": "#0f6cbf"
}
```

---

## 3. Rebuild & Synchronization Workflow

1. **Angular Web Build:**
   ```bash
   npm run build
   ```
   Compiles Angular TypeScript, SCSS, and injects updated `moodle.config.json` constants into the production web bundle (`www/`).

2. **Cordova Android Platform Sync:**
   ```bash
   npx ionic cordova prepare android
   ```
   Copies compiled web assets (`www/`) and native resources into `platforms/android/app/src/main/assets/www/`.

3. **Device Verification:**
   - Install fresh APK build on physical device/emulator.
   - Launch app: User is greeted by BDATA dark splash screen and taken directly to the **BDATA LMS** login screen (`https://moodle.bdata.com.mm`).

---

## 4. Evidence Artifacts

Collected files in this folder (`mobile-practice/T11/`):

| File | Description | Status |
|---|---|---|
| `device-login-theme.jpg` | Physical device screenshot showing the app pre-filled and connected to `https://moodle.bdata.com.mm` login screen. | [x] Collected |

---

## 5. Pass Criteria

- [x] Target LMS staging URL (`https://moodle.bdata.com.mm`) configured in `moodle.config.json`.
- [x] Application successfully built and synchronized to Android platform.
- [x] Physical device/emulator verification proves app connects directly to BDATA LMS.
- [x] Evidence screenshot captured and documented.

---

## PASS ✅
