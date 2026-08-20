# T06 — Authentication Setup

**Date:** 2026-08-19
**Branch:** `client/bdata-lms`
**Tag:** `v5.2.1`
**LMS Staging URL:** `https://moodle.bdata.com.mm`
**Authentication Type Configured:** Native (`Via the app`)

---

## 1. Objective

Configure and test mobile authentication methods in Moodle LMS (`Site administration → Mobile app → Mobile authentication`), understand the differences between login types (Native vs. Embedded Browser vs. System Browser), evaluate SSO / OAuth implications, and document QR code and auto-logout settings.

---

## 2. Login Types Overview & Analysis

| Login Type (`typeoflogin`) | Mechanism | Best Use Case | Pros & Cons |
|----------------------------|-----------|---------------|-------------|
| **Via the app (Native)** *(Current)* | Direct username/password form rendered in the mobile app UI. Requests token via `login/token.php`. | Standard manual accounts, email/username login, internal LDAP/DB. | **Pros:** Cleanest UX, fast, seamless.<br>**Cons:** Does not support OAuth2 (Google/MS) or 2FA plugins directly. |
| **Via an embedded browser** | Opens the web login page inside an in-app WebView / InAppBrowser overlay. | SAML, CAS, custom SSO plugins that support WebViews. | **Pros:** User stays inside the app window.<br>**Cons:** **Google OAuth blocks embedded WebViews** with `disallowed_useragent` error. |
| **Via a browser window (System Browser)** | Launches the default external mobile browser (Chrome/Safari) and passes the token back to the app via URL scheme (`moodlemobile://` or custom scheme). | Google OAuth2, Microsoft Entra ID (Office 365 SSO), OpenID Connect. | **Pros:** Fully compatible with Google/Apple/Microsoft security policies.<br>**Cons:** Context switch from app to browser and back. |

---

## 3. Configured Settings Summary (from Admin Screen)

From `Site administration → Mobile app → Mobile authentication`:

| Setting | Field Name (`tool_mobile`) | Configured Value | Default Value | Notes / Implications |
|---------|----------------------------|------------------|---------------|----------------------|
| **Type of login** | `typeoflogin` | `Via the app` | `Via the app` | Direct native in-app login form is active. |
| **Enforce auto logout** | `autologout` | `Never` | `Never` | User session token persists in app secure storage across app restarts. |
| **QR code access** | `qrcodetype` | `QR code with automatic login` | `QR code with automatic login` | Allows instant login by scanning QR code from user profile on web. |
| **QR auth key duration** | `qrkeyttl` | `10 minutes` | `10 minutes` | Generated QR code token remains valid for 10 minutes. |
| **QR auth same IP check** | `qrsameipcheck` | `Yes` (Checked) | `Yes` | Enforces scanning phone and generating PC to share the same public IP. |
| **URL scheme** | `forcedurlscheme` | `moodlemobile` | `moodlemobile` | Deep-linking scheme for browser authentication callback. |
| **Minimum app version** | `minimumversion` | *Empty* | *Empty* | No minimum app version restriction enforced. |
| **Auto-login min interval** | `autologinmintimebetweenreq` | `6 minutes` | `6 minutes` | Prevents rapid consecutive auto-login token regenerations. |

---

## 4. Testing Results

1. **Manual Username/Password Login (Native `Via the app`):**
   - Tested student account credentials (`aunglinnphyo`).
   - Token successfully issued by LMS and user successfully logged into the app.
   - Result: **PASS ✅**

2. **SSO / OAuth2 Assessment:**
   - Current staging setup uses manual native authentication.
   - If Google / Microsoft login is introduced in future client phases, `Type of login` must be switched to `Via a browser window` to comply with Google OAuth requirements.
   - Result: **Not in plan**

3. **QR Code Login Verification:**
   - `QR code with automatic login` tested on mobile app by scanning profile QR code.
   - User authenticated and logged into the LMS successfully via QR scanner.
   - Result: **PASS ✅**

4. **Auto-Logout Behaviour:**
   - Configured to `Never`. The user remains authenticated unless they explicitly tap **Log out** in app settings.

---

## 5. Evidence Artifacts (Screenshots)

Collected files in this folder (`mobile-practice/T06/`):

- [x] **`admin-settings.png`** — `Site administration → Mobile app → Mobile authentication` configuration screen showing `Via the app`, `Never` auto-logout, and QR settings.
- [x] **`site-connect.jpg`** — Mobile app connecting to `https://moodle.bdata.com.mm` site.
- [x] **`login-student-account.jpg`** — Mobile app native login screen for student account on `https://moodle.bdata.com.mm`.

---

## 6. Pass Criteria

- [x] Login type configured, analyzed, and documented (`Via the app`).
- [x] Manual username/password authentication verified on physical device.
- [x] Understanding of SSO / OAuth requirements (System Browser for Google/MS) documented.
- [x] QR code login and auto-logout policy verified.
- [x] Mobile authentication admin settings and login proof documented.

---

## PASS ✅
