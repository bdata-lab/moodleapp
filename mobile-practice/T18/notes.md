# T18 — Plugin & Activity Implementation Notes

**Task:** T18 — Plugin / activity implementation check  
**Branch:** `client/bdata-lms`  
**Target LMS:** `https://moodle.bdata.com.mm`  
**Date:** 2026-08-28  

---

## 1. RemUI vs Native App Boundary

### English:
> **RemUI vs Native App Boundary:**  
> RemUI is a web-based theme strictly for browsers, using complex HTML/CSS and custom components. The Moodle Native App, however, communicates via REST API to fetch only raw data and applies its own standardized mobile UI. Consequently, any RemUI-specific layouts or visual styling are completely stripped away in the app.

### မြန်မာဘာသာ:
> **RemUI နှင့် Native App အကြား ကွဲပြားချက် နယ်နိမိတ်:**  
> RemUI သည် Web Browser များအတွက်သာ သီးသန့်ရည်ရွယ်ထားသော Web-based Theme တစ်ခုဖြစ်ပြီး ရှုပ်ထွေးသော HTML/CSS နှင့် Custom UI Components များကို အသုံးပြုထားပါသည်။ သို့သော် Moodle Native App သည် Web Page တစ်ခုလုံးကို ဆွဲယူဖော်ပြခြင်းမဟုတ်ဘဲ REST API မှတစ်ဆင့် သန့်စင်သော Raw Data (JSON) များကိုသာ ဆွဲယူပြီး App ၏ Standardized Mobile UI ဖြင့်သာ ဖော်ပြပေးခြင်း ဖြစ်သည်။ ထို့ကြောင့် Web Browser ပေါ်တွင် RemUI ဖြင့် လှပခမ်းနားစွာ ပေါ်နေသော Course Layouts များနှင့် Visual Stylings များသည် Mobile App ထဲတွင် လုံးဝ ပါဝင်လာမည် မဟုတ်ဘဲ App ၏ သတ်မှတ်ပုံစံဖြင့်သာ ရိုးရိုးရှင်းရှင်း ပေါ်နေမည် ဖြစ်ပါသည်။

---

## 2. Technical Observations & Recommendations

1. **Native Mobile Activities:**
   - Activities such as Forums, Quizzes, Assignments, Pages, Books, and Attendance are rendered via native Angular/Ionic components in the mobile app, providing smooth offline caching and local interaction.
2. **In-Browser / In-App Browser (IAB) Fallbacks:**
   - Third-party packages like SCORM packages, BigBlueButton (BBB) live sessions, and certain complex H5P interactions or custom payment gateways fallback to In-App Browser or System Browser sessions using auto-login tokens.
3. **Theming Expectations for Clients:**
   - Clients must be informed early during kickoff that purchasing/installing Edwiser RemUI for their web portal does not customize the mobile app UI. Mobile branding requires source-level SCSS and mobile assets configuration.
