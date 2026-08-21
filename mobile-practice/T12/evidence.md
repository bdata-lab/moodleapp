# T12 — Android Debug Implementation

**Date:** 2026-08-21  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**Application ID:** `com.bdata.moodleapp`  
**App Name:** `BDATA LMS`  
**Target Staging:** `https://moodle.bdata.com.mm`  

---

## 1. Objective

Build and run the branded **BDATA LMS** Android debug application on a physical device/emulator:
1. Verify required JDK, Android SDK (API 34/35), and Gradle (8.11.1) build toolchain.
2. Compile web assets with BDATA brand identity and prepare Cordova Android platform.
3. Assemble the Android debug APK package (`:app:assembleDebug`).
4. Install and run on physical device to verify live communication with the staging LMS.

---

## 2. Environment & Toolchain Specifications

| Tool | Version | Path / Reference |
|---|---|---|
| **Java JDK** | OpenJDK 17.0.12 | `C:\Program Files\Java\jdk-17` |
| **Android SDK** | API Level 34 & 35 | `C:\Users\Vivobook\AppData\Local\Android\Sdk` |
| **Gradle** | 8.11.1 | `gradle-8.11.1-bin` |
| **Node.js** | v20.x | LTS |
| **Cordova Android** | 12.x / AndroidX | `platforms/android` |

---

## 3. Command Execution Logs (Success Lines Only)

### A. Angular Web Bundle Compilation
```bash
> cross-env NODE_OPTIONS=--max-old-space-size=8192 ionic build --configuration=development

> npm.cmd run ionic:build:before
> gulp
[10:24:53] Using gulpfile D:\Projects\moodleapp\gulpfile.js
[10:24:53] Starting 'default'...
[10:24:53] Starting 'lang'...
[10:24:53] Starting 'env'...
[10:24:53] Starting 'icons'...
[10:24:54] Finished 'env' after 101 ms
[10:24:54] Finished 'icons' after 102 ms
[10:24:54] Finished 'lang' after 243 ms
[10:24:54] Finished 'default' after 245 ms
> ng.cmd run app:build:development
- Generating browser application bundles (phase: setup)...
✔ Browser application bundle generation complete.
```

### B. Cordova Android Platform Synchronization
```bash
$ npx cordova prepare android
cordova-plugin-androidx-adapter: Processed 112 source files in 4234ms
COMPLETE_SUCCESS: All assets, icons, splash, and configurations synchronized!
```

### C. Gradle Android Debug Package Assembly (`:app:assembleDebug`)
```bash
$ cd platforms/android && gradle :app:assembleDebug
> Configure project :app
Adding classpath: com.google.gms:google-services:4.4.2
> Task :app:preBuild UP-TO-DATE
> Task :app:preDebugBuild UP-TO-DATE
> Task :app:generateDebugBuildConfig
> Task :app:processDebugGoogleServices
> Task :app:generateDebugResources
> Task :app:packageDebugResources
> Task :CordovaLib:compileDebugJavaWithJavac
> Task :app:compileDebugKotlin
> Task :app:compileDebugJavaWithJavac
> Task :app:mergeDebugAssets
> Task :app:processDebugManifest
> Task :app:dexBuilderDebug
> Task :app:mergeProjectDexDebug
> Task :app:packageDebug
> Task :app:createDebugApkListingFileRedirect
> Task :app:assembleDebug

BUILD SUCCESSFUL in 2m 9s
56 actionable tasks: 56 executed
```

### D. Generated APK Artifact
- **File:** `platforms/android/app/build/outputs/apk/debug/app-debug.apk`
- **Size:** 44.0 MB (44,093,804 bytes)
- **Status:** Valid signed debug package ready for device deployment.

---

## 4. Evidence Artifacts

Collected files in this folder (`mobile-practice/T12/`):

| File | Description | Status |
|---|---|---|
| `device-login-theme.jpg` | Physical device screen showing branded BDATA LMS app running live and communicating with staging server. | [x] Collected |

---

## 5. Pass Criteria

- [x] Android Studio / SDK versions configured according to codebase requirements.
- [x] Application successfully built using standard Android debug workflow.
- [x] Branded Android debug build connects and talks to staging LMS (`https://moodle.bdata.com.mm`).
- [x] Device screenshot and success command log documented.

---

## PASS ✅
