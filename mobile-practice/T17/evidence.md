# T17 — Restrict Site to Branded App (`forcedurlscheme`)

**Date:** 2026-08-25  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**Application ID:** `com.bdata.moodleapp`  
**Configured Scheme:** `bdatalms`  
**Target Staging:** `https://moodle.bdata.com.mm`  

---

## 1. Objective

Configure and test URL Scheme restriction (`forcedurlscheme`) on Moodle LMS:
1. Restrict mobile access so only the custom branded **BDATA LMS App** (`bdatalms://`) is permitted to connect.
2. Confirm that the **Official Moodle App** (`moodlemobile://`) is blocked from connecting.
3. Confirm that the **Branded BDATA LMS App** logs in successfully.
4. Understand and document the operational risks and support overhead associated with this setting.

---

## 2. Implementation Steps

### Step 1: LMS Admin Configuration
1. Log in to Moodle as Site Administrator.
2. Navigate to: `Site administration → Server → Mobile app → Mobile authentication`.
3. Set **URL scheme (`forcedurlscheme`)** to: `bdatalms`.
4. Click **Save changes**.

### Step 2: Verification with Official Moodle App (Blocked)
1. Open the standard **Official Moodle App** (from Google Play Store).
2. Enter site URL `https://moodle.bdata.com.mm` (or scan QR code).
3. **Result:** The server detects scheme mismatch (`moodlemobile://` vs required `bdatalms://`) and blocks the connection with an unauthorized error.

### Step 3: Verification with Branded BDATA App (Allowed)
1. Open the custom **BDATA LMS App** (`com.bdata.moodleapp`).
2. Connect to `https://moodle.bdata.com.mm`.
3. **Result:** The app matching `bdatalms://` scheme passes authentication and logs in successfully.

### Step 4: Revert / Retention
- **Staging Test:** Setting verified and documented.
- **Production Policy:** Keep `forcedurlscheme` set to `bdatalms` if the organization mandates exclusive use of the private branded app; otherwise leave blank to maintain dual compatibility.

---

## 3. Risk Explanation (Pass Condition)

As documented in [`notes.md`](./notes.md):

> **Risk Summary:**
> If `forcedurlscheme` is enabled on production, any learners who attempt to log in using the standard Official Moodle App downloaded from the Play Store / App Store will be blocked. This creates a significant IT support overhead, as users may assume the server is down or their credentials are invalid. The IT team must then individually instruct users to uninstall the official app and install the private BDATA LMS app.

---

## 4. Evidence Artifacts

Files stored in this folder (`mobile-practice/T17/`):

| File | Description | Status |
|---|---|---|
| [`notes.md`](file:///d:/Projects/moodleapp/mobile-practice/T17/notes.md) | Technical risk analysis and support overhead documentation in English & Burmese. | [x] Completed |
| `device-blocked-alert.jpg` | Screenshot of Official Moodle App showing blocked alert due to scheme mismatch. | [x] Collected |
| `device-dashboard.jpg` | Screenshot of Branded BDATA LMS App successfully authenticated and on Dashboard. | [x] Collected |

---

## 5. Pass Criteria

- [x] Configured `forcedurlscheme` to `bdatalms` in Moodle Mobile authentication.
- [x] Verified Official Moodle App is blocked due to URL scheme mismatch.
- [x] Verified Branded BDATA LMS App connects and logs in smoothly.
- [x] Clear risk analysis and support overhead explanation documented in `notes.md`.
- [x] Evidence files organized in `mobile-practice/T17/`.

---

## PASS ✅
