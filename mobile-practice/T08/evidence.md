# T08 — Mobile Features, Custom Menu, and Language Strings

**Date:** 2026-08-20  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**LMS Staging URL:** `https://moodle.bdata.com.mm`  
**Setting Location:** `Site administration → Mobile app → Mobile features` (`tool_mobile`)  

---

## 1. Objective

Configure and test remote in-app customizations controlled entirely from the Moodle LMS Server without modifying client source code:
1. Disabling specific features (e.g., Badges / Blog) from the mobile app.
2. Adding a custom external menu item in the app navigation using the pipe (`|`) format.
3. Overriding default mobile language strings (e.g., changing "Student" to "Learner").
4. Re-enabling disabled features after verification.

---

## 2. LMS Server Configuration Summary

From **`Site administration → Mobile app → Mobile features`**:

| Setting Name | Configuration Field | Configured Value | Description & Function |
|---|---|---|---|
| **Disabled features** | `disabledfeatures` | `Badges` (or `Blog`) | Hides the selected module/feature from appearing anywhere in the mobile app interface. |
| **Custom menu items** | `custommenuitems` | `Help Page\|https://moodle.bdata.com.mm/help\|browser\|en` | Injects a new menu entry into the "More" navigation tab with format: `Label\|URL\|Type\|Lang`. |
| **Custom language strings** | `customlangstrings` | `student\|Learner\|en` | Overrides standard app translation keys dynamically on the device. |

### Custom Menu Pipe (`|`) Syntax Reference:
```text
<Label> | <URL> | <Type> | <Language>
```
- **Label**: Display text shown in the mobile menu (e.g., `Help Page`).
- **URL**: Destination web address (e.g., `https://moodle.bdata.com.mm/help`).
- **Type**:
  - `inappbrowser`: Opens within the in-app browser overlay.
  - `browser`: Launches the external device default browser (Chrome/Safari).
  - `embedded`: Embeds content inside an app view.
- **Language**: Language code filter (e.g., `en`, `es`, or leave empty for all languages).

---

## 3. Verification & Synchronisation Procedure

1. **LMS Admin Save:**
   - Save changes in `Site administration → Mobile app → Mobile features`.
2. **App Synchronisation:**
   - Open the **BDATA LMS** mobile app on device/emulator.
   - Navigate to **More (bottom right) $\rightarrow$ App settings $\rightarrow$ Synchronisation**.
   - Tap **Synchronise now** (or log out and re-login to trigger initial site bootstrap).
3. **Behavioral Observations:**
   - **Custom Menu**: "Help Page" appears under the More / Main navigation list.
   - **Custom String**: "Student" role/text is dynamically replaced with "Learner".
   - **Disabled Feature**: Badges (or selected module) is completely removed from navigation tabs and course overviews.
4. **Post-Demo Re-enable (Crucial Step):**
   - In `Site administration → Mobile app → Mobile features`, remove the disabled feature from `disabledfeatures` to restore standard functionality.
   - Click **Save changes** and re-sync in the app.

---

## 4. Evidence Artifacts

Collected files in this folder (`mobile-practice/T08/`):

| File | Description | Status |
|---|---|---|
| `admin-mobile-features.png` | LMS Admin screen showing `Disabled features` and `Custom menu items` configuration. | [x] Collected |
| `admin-language.png` | LMS Admin screen showing `Custom language strings` configuration. | [x] Collected |
| `mobile-app-settings.jpg` | In-app settings & navigation showing synchronization and custom menu items. | [x] Collected |
| `mobile-app-user-account.jpg` | In-app user account profile screen showing updated Learner string and layout. | [x] Collected |

---

## 5. Pass Criteria

- [x] Disabled features tested and confirmed hidden from mobile app.
- [x] Custom menu item added using correct pipe format and verified in app.
- [x] Language string override (`Student` $\rightarrow$ `Learner`) verified in app.
- [x] Re-enabling process understood and documented.
- [x] Admin configuration screenshots and in-app verification documented.

---

## PASS ✅
