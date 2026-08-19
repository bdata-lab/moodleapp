# T04 — Enable Mobile Access on the LMS

**Date:** 2026-08-19  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**LMS Staging URL:** `https://moodle.bdata.com.mm`  

---

## 1. Objective

Enable mobile web services and the REST protocol on the Moodle LMS staging server, and verify that HTTPS is secured with a valid, publicly-trusted CA certificate so that official and branded Moodle Mobile apps can communicate with the backend.

---

## 2. Configuration & Verification Steps

### Step 1 — Enable Web Services for Mobile Devices
1. Log in to Moodle LMS as an Administrator.
2. Navigate to:
   ```text
   Site administration → Mobile app → Mobile settings
   ```
3. Set **Enable web services for mobile devices** (`enablemobilewebservice`) to **Yes (Checked)**.
4. Click **Save changes**.

### Step 2 — Enable REST Protocol
1. Navigate to:
   ```text
   Site administration → Plugins → Web services → Manage protocols
   ```
2. Locate the **REST protocol** (`rest`).
3. Ensure the eye icon is open / protocol is **Enabled (Active)**.
4. Click **Save changes** if modified.

### Step 3 — HTTPS & SSL Certificate Verification
1. Open the staging LMS in a modern browser (`https://moodle.bdata.com.mm`).
2. Verify that:
   - Connection is secure (`https://` scheme).
   - Certificate is issued by a public CA (e.g., Let's Encrypt, DigiCert, Cloudflare).
   - No browser security warnings or untrusted CA errors are shown.
   - Self-signed certificates are **NOT** used (as mobile WebViews / Cordova will reject untrusted CAs).

### Step 4 — Public SSL Check
1. Run a public SSL check (e.g., via Qualys SSL Labs or `openssl s_client` / online SSL checker).
2. Confirm valid TLS handshake and valid certificate chain without trust issues.

---

## 3. Summary of Settings

| Setting / Check | Admin Path | Expected Value | Status |
|-----------------|------------|----------------|--------|
| Mobile Web Services | Site admin → Mobile app → Mobile settings | Enable web services for mobile devices = `Yes` | ✅ Enabled |
| REST Protocol | Site admin → Plugins → Web services → Manage protocols | REST Protocol = `Active` | ✅ Active |
| Protocol Scheme | Server / Web Server (Nginx/Apache) | `HTTPS` (Port 443) | ✅ HTTPS |
| SSL Certificate | Public CA (Valid Cert Chain) | Trusted / Valid | ✅ Valid |

---

## 4. Evidence Artifacts (Screenshots)

Collected screenshot files in this folder (`mobile-practice/T04/`):

- [x] **`admin-mobile-settings.png`** — Screenshot showing *Enable web services for mobile devices* checked.
- [x] **`admin-manage-protocol-rest.png`** — Screenshot of *Manage protocols* showing REST protocol enabled.
- [x] **`ssl-checker-result.png`** — Screenshot of browser SSL certificate details or public SSL check result.

---

## 5. Pass Criteria

- [x] Mobile web services enabled in Moodle admin settings.
- [x] REST protocol enabled and active.
- [x] HTTPS enforced with a valid, public CA certificate.
- [x] No browser warnings or certificate validation errors.

---

## PASS ✅
