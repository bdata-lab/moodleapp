# T05 — Connect the Official Moodle App (Baseline)

**Date:** 2026-08-19  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**LMS Staging URL:** `https://moodle.bdata.com.mm`  
**Test Client:** Official Moodle App (Store version)  
**Test Account Role:** Student  

---

## 1. Objective

Verify that the Moodle LMS staging server (`https://moodle.bdata.com.mm`) connects properly with the official store version of the Moodle App as a baseline prior to building and testing any custom branded binaries. Ensure authentication, Web Services, and course rendering function without errors.

---

## 2. Testing Steps Completed

### Step 1 — Site Connection
1. Launched the official Moodle App on a physical mobile device.
2. Entered the staging site URL:
   ```text
   https://moodle.bdata.com.mm
   ```
3. Confirmed the site was resolved successfully via HTTPS without SSL handshake or network errors.

### Step 2 — Authentication (Student Account)
1. Entered student credentials on the login screen.
2. Successfully authenticated with the LMS via the official mobile authentication flow (`login/token.php`).
3. User session initialized and user profile loaded.

### Step 3 — Navigation & Course List Verification
1. Navigated to **My courses / Dashboard**.
2. Confirmed enrolled courses list loaded accurately.
3. Accessed course content to verify sections, activities, and resources load without WebService errors.

---

## 3. Test Results Summary

| Check Item | Description | Result |
|------------|-------------|--------|
| Site Discovery & SSL | Connected to `https://moodle.bdata.com.mm` | ✅ Pass |
| Mobile Authentication | Authenticated test student user | ✅ Pass |
| Course Overview | Loaded enrolled course list in app | ✅ Pass |
| Core WebServices | `tool_mobile` & core APIs returned valid data | ✅ Pass |

---

## 4. Evidence Artifacts (Screenshots)

Collected device screenshots in this folder (`mobile-practice/T05/`):

- [x] **`site-connect.jpg`** — App connecting to the staging LMS URL.
- [x] **`login-student-account.jpg`** — Student login screen / credentials entry.
- [x] **`course-list.jpg`** — Enrolled courses / My courses view after successful login.

---

## 5. Pass Criteria

- [x] Official Moodle App installed from the official store.
- [x] Successfully connected to the staging LMS (`https://moodle.bdata.com.mm`).
- [x] Student login authenticated successfully.
- [x] Student can view enrolled courses and navigate course content.
- [x] Verified LMS mobile baseline functionality is healthy before custom branding.

---

## PASS ✅
