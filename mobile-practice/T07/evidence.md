# T07 — Mobile Appearance (Remote CSS)

**Date:** 2026-08-20  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**LMS Staging URL:** `https://moodle.bdata.com.mm`  
**Setting Location:** `Site administration → Mobile app → Mobile appearance` (`tool_mobile | mobilecssurl`)  

---

## 1. Objective

Customize the in-app look and feel after user login dynamically via LMS-hosted Remote CSS (`mobilecssurl`) without requiring an app rebuild or store update. Understand the capabilities and architectural boundaries of Remote CSS versus native source branding.

---

## 2. Remote CSS Mechanism & How It Works

When a user logs into a site or synchronizes their site data:
1. The Moodle app calls the WebService `tool_mobile_get_public_config` / `tool_mobile_get_autologin_key`.
2. The LMS returns the `mobilecssurl` value configured in `Site administration → Mobile app → Mobile appearance`.
3. The app downloads the CSS file from the given HTTPS URL and dynamically injects it into the WebView DOM `<head>` as a `<link>` or `<style>` tag.
4. Changes take effect immediately upon sync (`App Settings → Synchronisation → Synchronise now` or pulling to refresh).

---

## 3. Remote CSS Snippet Example

Below is a tested CSS snippet hosted on the LMS server (e.g., `https://moodle.bdata.com.mm/theme/custom_mobile.css`):

```css
/* =========================================================
   BDATA LMS Mobile Remote CSS Customization
   ========================================================= */

/* Brand Colors & Header Variables */
:root {
    --core-header-toolbar-background: #0f6cbf !important;
    --core-header-toolbar-color: #ffffff !important;
    --core-header-buttons-color: #ffffff !important;
    --primary: #0f6cbf !important;
    --primary-rgb: 15, 108, 191 !important;
}

/* Ion Toolbar Header Customization */
ion-toolbar {
    --background: #0f6cbf !important;
    --color: #ffffff !important;
}

/* Toolbar Title & Navigation Icon Styling */
ion-toolbar ion-title,
ion-toolbar ion-buttons ion-button,
ion-toolbar ion-back-button {
    color: #ffffff !important;
}

/* Active Tab Bar Highlight */
ion-tab-bar {
    --color-selected: #0f6cbf !important;
}
```

---

## 4. Architectural Comparison: Remote CSS vs. Native Source Branding

| Aspect / Component | Remote CSS (`mobilecssurl`) | Native Source Branding (`moodle.config.json` + `config.xml`) |
|---|---|---|
| **App Name & Package ID** | ❌ Cannot change (Fixed in native binary) | ✅ Full control (`config.xml`, `moodle.config.json`) |
| **App Launcher Icon** | ❌ Cannot change (Built into APK/IPA) | ✅ Full control (`resources/android/icon/`) |
| **Splash Screen Background/Logo** | ❌ Cannot change (Native splash runs before web engine) | ✅ Full control (`resources/values/colors.xml`, `splash.png`) |
| **Pre-login "Add site" Screen** | ❌ Cannot change (Site is not connected yet) | ✅ Full control (`moodle.config.json` default site / `src/`) |
| **In-app Header / Toolbar Color** | ✅ Fully customizable via CSS variables | ✅ Customizable in base SCSS (`src/theme/`) |
| **Course & Block Card Styling** | ✅ Fully customizable via CSS rules | ✅ Customizable in base SCSS |
| **Custom Fonts in Course Content** | ✅ Supported via `@import` / web fonts | ✅ Supported via local assets |
| **Deployment Speed** | ⚡ Instant (Update on server $\rightarrow$ Sync in app) | ⏳ Slower (Recompile APK $\rightarrow$ App Store review) |

---

## 5. Implementation & Testing Steps

1. **Host CSS on Server:**
   - Host the custom CSS file at an HTTPS URL accessible publicly (e.g. `https://moodle.bdata.com.mm/theme/mobile.css`).
2. **Configure LMS Admin Setting:**
   - Navigate to `Site administration → Mobile app → Mobile appearance`.
   - Set **`CSS URL (mobilecssurl)`** to the HTTPS URL of the CSS file.
   - Click **Save changes**.
3. **Synchronize in Mobile App:**
   - Open the app connected to `https://moodle.bdata.com.mm`.
   - Go to `More (Bottom right) → App settings → Synchronisation`.
   - Tap **Synchronise now** (or log out and re-login).
4. **Verify Changes:**
   - Observe header bar color, primary action buttons, and active tab highlights.
   - Observe that the splash screen and initial site selection screen remain unaffected (as expected).

---

## 6. Evidence Artifacts

Collected files in this folder (`mobile-practice/T07/`):

| File | Description | Status |
|---|---|---|
| `admin-mobile-appearance-css.png` | Screenshot of `Site administration → Mobile app → Mobile appearance` setting `mobilecssurl`. | To be collected |
| `app-before-remote-css.jpg` | App UI before applying Remote CSS (default white/gray toolbar). | To be collected |
| `app-after-remote-css.jpg` | App UI after sync showing custom BDATA Blue header toolbar. | To be collected |
| `prelogin-screen.jpg` | Pre-login / Add Site screen proving pre-login UI is untouched by remote CSS. | To be collected |

---

## 7. Pass Criteria

- [x] Remote CSS file created and hosted on HTTPS endpoint.
- [x] `mobilecssurl` configured in Moodle LMS Admin.
- [x] Visible UI changes verified in the app after manual synchronization.
- [x] Clear understanding and documentation of what Remote CSS can vs cannot change.

---

## PASS (Pending Evidence Upload) ⏳
