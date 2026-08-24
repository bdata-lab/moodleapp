# T13 — Android Release Package (Signed Release APK)

**Date:** 2026-08-24  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**Application ID:** `com.bdata.moodleapp`  
**App Name:** `BDATA LMS`  
**Target Staging:** `https://moodle.bdata.com.mm`  

---

## 1. Objective

Generate an installable, signed Android production release artefact (`app-release.apk`):
1. Create a secure keystore outside the Git repository.
2. Build and sign the production release APK using Android Studio / Gradle release toolchain.
3. Sideload and install the signed release APK onto a physical Android device.
4. Verify authentication with the staging LMS and check the version information in the in-app **About** / **App settings** screen.

---

## 2. Release Package Artefact Specifications

| Property | Value | Description |
|---|---|---|
| **Artefact File** | `app-release.apk` | Signed release APK package |
| **Output Location** | `platforms/android/app/release/app-release.apk` | Build release directory |
| **Package ID** | `com.bdata.moodleapp` | BDATA LMS unique application namespace |
| **Version Name** | `5.2.1` | Client release semantic version |
| **Version Code** | `52100` | Integer build version code |
| **File Size** | `38,027,612 bytes (38.0 MB)` | Standalone compressed release binary |
| **Signing Variant** | `release` (V1 + V2/V3 scheme) | Signed with secure Keystore |
| **Target SDK** | `API 34 / 35` | Android 14 / 15 compatibility |

---

## 3. Keystore & Build Workflow

1. **Keystore Generation (Stored securely outside Git):**
   - Generated signing key with RSA 2048-bit key size and 25-year validity.
   - Keystore file is excluded from Git tracking via `.gitignore` to protect signing credentials.

2. **Release APK Generation:**
   - Compiled production web bundle: `npm run build`
   - Synchronized platform assets: `npx cordova prepare android`
   - Generated signed release package in Android Studio: `Build > Generate Signed Bundle / APK > APK` (or `./gradlew :app:assembleRelease`)
   - Output produced at `platforms/android/app/release/app-release.apk`.

3. **Device Verification:**
   - Sideloaded `app-release.apk` onto physical Android device.
   - Launched app: Dark splash screen and BDATA Blue theme loaded successfully.
   - Authenticated with student account on `https://moodle.bdata.com.mm`.
   - Verified version number and build code under **App settings > About**.

---

## 4. Evidence Artifacts

Collected files in this folder (`mobile-practice/T13/`):

| File | Description | Status |
|---|---|---|
| `device-version.jpg` | Physical device screen showing installed release APK version (`5.2.1 / 52100`) and successful login. | [x] Collected |

---

## 5. Pass Criteria

- [x] Development/Release Keystore created and stored outside Git repository.
- [x] Signed release APK (`app-release.apk`) generated successfully.
- [x] Release APK installed on physical device (sideloaded without debug bridge).
- [x] Application logs in and communicates with staging LMS (`https://moodle.bdata.com.mm`).
- [x] Version name (`5.2.1`) and version code (`52100`) verified on device About screen.
- [x] Release package metadata and device screenshot documented.

---

## PASS ✅
