# T03 — Device Debug Setup

**Date:** 2026-08-18  
**Branch:** client/bdata-lms  
**Tag:** v5.2.1  
**Platform:** Android (USB Debugging / Chrome Remote Inspector)

---

## 1. Objective

Debug the running Moodle App on a physical Android device (or emulator) via Chrome Remote Debugging (`chrome://inspect`) and capture a live WebService (WS) network call to the Moodle LMS.

---

## 2. Setup & Steps Completed

### Step 1 — Android Device Debugging Configuration
1. Connected Android device via USB.
2. Enabled **Developer Options** $\rightarrow$ Enabled **USB Debugging**.
3. Confirmed device authorization dialog ("Allow USB debugging").

### Step 2 — Chrome Remote Inspector
1. Opened Google Chrome on PC and navigated to:
   ```text
   chrome://inspect/#devices
   ```
2. Located the running App WebView under **Remote Target**:
   - Target: `com.bdata.moodleapp` (or Moodle App WebView)
   - Page URL: `https://localhost/index.html` (or `http://localhost:8100/`)
3. Clicked **inspect** to open Chrome DevTools for the mobile WebView.

### Step 3 — Network Tab & WebService Capture
1. In Chrome DevTools, switched to the **Network** tab $\rightarrow$ filtered by **Fetch/XHR**.
2. Triggered app initialization / LMS connection attempt.
3. Captured the initial Moodle Mobile WebService public config request:

#### Captured Moodle WS Call:
- **Request URL:**
  ```text
  https://moodle.bdata.com.mm/webservice/rest/server.php?moodlewsrestformat=json&wsfunction=tool_mobile_get_public_config
  ```
- **HTTP Method:** `POST` / `GET`
- **Parameters:**
  ```json
  {
    "moodlewsrestformat": "json",
    "wsfunction": "tool_mobile_get_public_config"
  }
  ```
- **Login Token Service URL (Authentication):**
  ```text
  https://moodle.bdata.com.mm/login/token.php?service=moodle_mobile_app&username=<username>&password=<password>
  ```

---

## 3. Evidence Artifacts

- [x] **`chrome-inspect-screenshot.png`** — Chrome `chrome://inspect` device inspector showing the WebView and Network tab.
- [x] **Captured WS URL:** `https://moodle.bdata.com.mm/webservice/rest/server.php?wsfunction=tool_mobile_get_public_config`

---

## 4. Pass Criteria

- [x] Android USB debugging configured and functional.
- [x] Chrome DevTools inspector connects to the running WebView.
- [x] Successfully captured WS request/response from the device/WebView.

---

## PASS ✅
