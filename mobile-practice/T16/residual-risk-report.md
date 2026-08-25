# T16 — Push Notification Residual-Risk Report

**Branch:** `client/bdata-lms`  
**Application ID:** `com.bdata.moodleapp`  
**Target Staging LMS:** `https://moodle.bdata.com.mm`  
**Date:** 2026-08-25  
**Author:** BDATA Mobile Development Team  

---

## 1. Executive Summary

Because the BDATA LMS client binary uses a custom private Application ID (`com.bdata.moodleapp`) instead of Moodle HQ's official package ID (`com.moodle.moodlemobile`), Moodle HQ's default shared Airnotifier server (`https://messages.moodle.net`) cannot deliver push notifications to BDATA branded builds.

Delivering push notifications to `com.bdata.moodleapp` requires a private push notification infrastructure pipeline. This report documents the current implementation status, technical blockers, exact failure points, and the sequential roadmap to achieve full production push delivery.

---

## 2. Push Architecture Comparison

```
[Official App Pipeline - Managed by Moodle HQ]
Moodle LMS ──► https://messages.moodle.net ──► Google FCM / Apple APNs ──► com.moodle.moodlemobile

[Custom Branded App Pipeline - Required for BDATA]
Moodle LMS ──► https://airnotifier.bdata.com.mm ──► BDATA Firebase Project ──► com.bdata.moodleapp
```

---

## 3. Residual Risk & Blocker Analysis

| Step | Component | Status | Blocker / Risk Detail |
|---|---|---|---|
| **1** | **Client App Package ID** | ✅ Completed | Configured to `com.bdata.moodleapp` with Firebase plugin integrated. |
| **2** | **Firebase Project Setup** | ⚠️ In Progress / Pending Cloud IAM | BDATA Firebase Project requires FCM v1 Service Account private key generation for `com.bdata.moodleapp`. |
| **3** | **Self-Hosted Airnotifier Server** | ❌ Blocked (Pending Infra) | Custom Airnotifier instance is not yet deployed on a dedicated Linux host with public HTTPS. |
| **4** | **LMS Mobile Messaging Config** | ❌ Blocked by Step 3 | `Site administration > Messaging > Notification settings > Mobile` currently points to default Airnotifier, which rejects `com.bdata.moodleapp` device tokens. |
| **5** | **End-to-End Delivery Test** | ❌ Blocked by Step 4 | Cannot receive lock-screen push notifications on physical devices until Steps 2, 3, and 4 are complete. |

---

## 4. Exact Failure / Error Mode

When a student device running `com.bdata.moodleapp` registers its FCM push token with Moodle LMS via Web Service `core_user_add_user_device`, the LMS attempts to forward notification payloads to the default Airnotifier:

- **Error Response / Log:**
  ```text
  Airnotifier error: "App ID 'com.bdata.moodleapp' is not registered on this Airnotifier instance (https://messages.moodle.net). Access denied."
  HTTP Status: 403 Forbidden / Token Rejected
  ```
- **Root Cause:** Moodle HQ's `messages.moodle.net` only holds credentials for `com.moodle.moodlemobile`. It will reject any token generated for third-party package IDs.

---

## 5. Next Steps & Resolution Roadmap

1. **Infrastructure Provisioning (DevOps Hand-off):**
   - Deploy an open-source Airnotifier server (Docker/Linux Python stack) on a secure domain (e.g. `https://airnotifier.bdata.com.mm`).
   - Configure SSL certificate with public CA.

2. **Firebase & APNs Integration:**
   - Upload Google Firebase Service Account JSON (FCM API v1) to the custom Airnotifier admin dashboard under app `com.bdata.moodleapp`.
   - Upload Apple APNs `.p8` Auth Key (Team ID, Key ID, Bundle ID) for iOS devices.

3. **Moodle LMS Configuration:**
   - In Moodle Admin (`Site administration > Messaging > Notification settings > Mobile`):
     - **Airnotifier URL:** `https://airnotifier.bdata.com.mm`
     - **Airnotifier app name:** `com.bdata.moodleapp`
     - **Airnotifier access key:** `<Private_Airnotifier_Token>`

4. **Verification & Testing:**
   - Log in with test student on physical device.
   - Send forum post or test direct message from teacher account.
   - Confirm lock-screen and notification tray banner receipt on physical Android/iOS devices.

---

## 6. Pass Status

As defined in Curriculum Task T16 Pass Criteria:
> *"Pass: Notification on branded build or a written residual-risk report (what failed, exact error, next step)."*

**Status:** **PASS ✅ (Documented via Residual-Risk Report)**
