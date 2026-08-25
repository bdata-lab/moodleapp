# T17 — Forced URL Scheme Risk Analysis Notes

**Task:** T17 — Restrict site to the branded app (`forcedurlscheme`)  
**Configured Scheme:** `bdatalms`  
**Target LMS:** `https://moodle.bdata.com.mm`  
**Date:** 2026-08-25  

---

## 1. Technical Mechanism

When `forcedurlscheme` is set to `bdatalms` under `Site administration → Mobile app → Mobile authentication`:
- Moodle LMS injects the required URL scheme check into the mobile authentication response and deep-linking handlers.
- The **Official Moodle App** (which only registers and listens to the default `moodlemobile://` scheme) is detected as an unauthorized client. The LMS blocks login and issues a scheme mismatch error.
- The **Branded BDATA LMS App** (which registers `bdatalms://` in `config.xml` and `moodle.config.json`) matches the server's required scheme and is granted full login access.

---

## 2. Risk Explanation (အန္တရာယ် ရှင်းလင်းချက်)

### English:
> If `forcedurlscheme` is enabled on production, any learners who attempt to log in using the standard Official Moodle App downloaded from Google Play Store or Apple App Store will be immediately blocked from connecting.
>
> This creates significant IT support overhead, as users may assume the LMS server is down or their accounts are broken. The IT support team must then provide 1-on-1 assistance explaining that the official app must be uninstalled and replaced with the private BDATA LMS mobile app.

### မြန်မာဘာသာ:
> "အကယ်၍ ဤ `forcedurlscheme` ကို ဖွင့်ထားမည်ဆိုပါက၊ Play Store မှ Official Moodle App ကို အလွယ်တကူ ဒေါင်းလုဒ်ဆွဲပြီး ဝင်ရောက်ရန် ကြိုးစားသော ကျောင်းသားများအားလုံး ဝင်ခွင့်ရမည်မဟုတ်ဘဲ အခက်အခဲ တွေ့ကြပါမည်။
>
> ထိုအခါ ကျောင်း၏ IT Support Team ထံသို့ 'App ထဲ ဝင်လို့မရဘူး' ဆိုသည့် တိုင်ကြားမှုများ အလုံးအရင်း ရောက်လာနိုင်ပါသည်။ ကျောင်းသားတိုင်းကို 'Official App ဖျက်ပါ၊ BDATA App ကို ပြောင်းသွင်းပါ' ဟု လိုက်လံရှင်းပြနေရမည့် Support ပေးရသော ဝန်ထုပ်ဝန်ပိုး (Support overhead) ကြီးမားသွားနိုင်ပါသည်။"

---

## 3. Operational Recommendation

- **Staging / Testing:** Enable temporarily to verify that official app blocking and branded app bypass work as designed, then revert to empty unless the client explicitly mandates a single-app policy.
- **Production:** Only enable if all end-user distribution channels exclusively direct learners to the branded BDATA LMS app.
