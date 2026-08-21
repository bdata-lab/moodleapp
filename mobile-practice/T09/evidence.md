# T09 — App Banners, Download Link, and Store Identifiers

**Date:** 2026-08-21  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**LMS Staging URL:** `https://moodle.bdata.com.mm`  
**Setting Location:** `Site administration → Mobile app → Mobile appearance` (`tool_mobile`)  

---

## 1. Objective

Configure website smart app banners, app download page redirection, and platform-specific unique identifiers (Android Package ID and iOS App Store ID) on the Moodle LMS. Understand the exact operational changes required when transitioning from official baseline app links to a custom client-branded app (`BDATA LMS`).

---

## 2. LMS Configuration Summary

From **`Site administration → Mobile app → Mobile appearance`**:

| Setting Name | Field Key (`tool_mobile`) | Baseline Configured Value | Future Custom Branded Value | Description / Purpose |
|---|---|---|---|---|
| **App download page** | `setuplink` | `https://download.moodle.org/mobile` | `https://moodle.bdata.com.mm` *(or custom landing page)* | The web link displayed in the user profile and footer directing learners to download the app. |
| **iOS app's unique identifier** | `iosappid` | `633359593` *(Official Moodle)* | `<BDATA_Apple_App_ID>` *(e.g. 647xxxxxxx)* | App Store ID used by Safari Smart App Banners to prompt iOS users to open/install the app. |
| **Android app's unique identifier** | `androidappid` | `com.moodle.moodlemobile` *(Official)* | `com.bdata.moodleapp` | Google Play Store Package ID used by Chrome web banners to direct Android users to the exact app. |

---

## 3. How Smart App Banners Work (Mechanism)

1. **iOS Safari Smart Banner:**
   - When configured with `iosappid`, Moodle injects a `<meta name="apple-itunes-app" content="app-id=...">` tag into the HTML `<head>`.
   - iOS Safari detects this and displays a native system banner at the top of the browser prompting the learner to "OPEN" (if installed) or "VIEW" in App Store.
2. **Android Chrome Intent / Smart Banner:**
   - Chrome utilizes the `androidappid` and web manifest / deep link metadata to show an installation prompt or open the native app directly.

---

## 4. Production Transition Checklist (When BDATA LMS Ships to Stores)

When the custom branded **BDATA LMS** mobile app is compiled, signed, and published to Google Play Store and Apple App Store, the LMS administrator must update these settings:

1. **`androidappid`**: Change from `com.moodle.moodlemobile` $\rightarrow$ `com.bdata.moodleapp`.
2. **`iosappid`**: Change from `633359593` $\rightarrow$ Your assigned Apple App Store numeric ID.
3. **`setuplink`**: Update to your corporate download portal or smart redirect link (e.g. `https://moodle.bdata.com.mm/download`).

---

## 5. Evidence Artifacts

Collected files in this folder (`mobile-practice/T09/`):

| File | Description | Status |
|---|---|---|
| `admin-mobile-appearence.png` | LMS Admin screen showing `App download page`, `iosappid`, and `androidappid` settings configured. | [x] Collected |

---

## 6. Pass Criteria

- [x] App download page URL (`setuplink`) configured on LMS.
- [x] iOS and Android unique app identifiers (`iosappid`, `androidappid`) configured and understood.
- [x] Understanding of Smart App Banner mechanism documented.
- [x] Production transition requirements (updating to `com.bdata.moodleapp` and BDATA iOS App ID when published) clearly documented.
- [x] Evidence screenshot collected and verified.

---

## PASS ✅
