# T18 — Plugin & Activity Implementation Check

**Date:** 2026-08-28  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  
**Application ID:** `com.bdata.moodleapp`  
**Target LMS:** `https://moodle.bdata.com.mm`  

---

## 1. Objective

Test and evaluate what core Moodle activities and custom plugins work natively inside the BDATA LMS mobile app versus those that fallback to an in-app browser or external browser session. Document the critical architectural boundary between web themes (RemUI) and native mobile interfaces.

---

## 2. Activity & Plugin Implementation Matrix

| Activity / Feature | Result | Architecture / Experience Notes |
|---|---|---|
| **Course list / dashboard** | Native (Pass) | Enrolled courses, course progress cards, and dashboard render via native Angular components. |
| **File, Page, URL, Book** | Native (Pass) | Resources render natively with full offline reading and download capabilities. |
| **Forum** | Native (Pass) | Discussion topics, posts, and replies load and post natively without leaving the app. |
| **Quiz** | Native (Pass) | Question types, timers, attempt submission, and offline attempt caching supported. |
| **Assignment submit** | Native (Pass) | Submission status, deadlines, and file upload interface render natively. |
| **H5P** | Native (Pass) | Core H5P interactive content runs within integrated app player. |
| **SCORM** | In-browser / IAB (Pass) | SCORM packages require In-App Browser (IAB) execution due to legacy web runtime dependencies. |
| **BBB join** | In-browser (Fallback) | BigBlueButton virtual classroom sessions launch in external/system browser. |
| **Grades** | Native (Pass) | Gradebook user report and course totals displayed natively. |
| **Messaging** | Native (Pass) | In-app messaging, contact search, and instant communication render natively. |
| **CustomCertificate** | In-browser (Pass) | Certificate generation and PDF download trigger browser/document viewer. |
| **Attendance** | Native (Pass) | Attendance sessions, status points, and self-recording supported natively. |
| **Payment enrolment** | In-browser (Fallback) | Payment gateways redirect to system/in-app browser for secure payment gateway processing. |
| **Offline download** | Native (Pass) | Course sections and activity files can be downloaded for offline access. |
| **Myanmar language** | Native (Pass) | Unicode Myanmar font renders cleanly across native UI components. |
| **RemUI course layout** | Stripped / N/A (Pass) | Web-based RemUI layouts are ignored; rendered in standard native mobile course format. |

---

## 3. RemUI vs Native App Boundary

> **RemUI vs Native App Boundary:**  
> RemUI is a web-based theme strictly for browsers, using complex HTML/CSS and custom components. The Moodle Native App, however, communicates via REST API to fetch only raw data and applies its own standardized mobile UI. Consequently, any RemUI-specific layouts or visual styling are completely stripped away in the app.

---

## 4. Evidence Artifacts

Files stored in this folder (`mobile-practice/T18/`):

| File | Description | Status |
|---|---|---|
| [`notes.md`](file:///d:/Projects/moodleapp/mobile-practice/T18/notes.md) | RemUI vs Native App boundary statement and technical observations. | [x] Completed |
| `test-table.png` | Comprehensive test matrix table showing Pass/Fail/In-browser evaluations. | [x] Collected |
| `remui.jpg` | Physical device screenshot demonstrating standard native mobile layout stripping RemUI web styles. | [x] Collected |
| `Forum.jpg` | Physical device screenshot demonstrating native Forum discussion experience. | [x] Collected |
| `attendance.jpg` | Physical device screenshot demonstrating native Attendance activity. | [x] Collected |
| `SCORM.jpg` | Physical device screenshot demonstrating In-App Browser fallback for SCORM packages. | [x] Collected |

---

## 5. Pass Criteria

- [x] Activity & Plugin implementation table completed across all standard Moodle activities.
- [x] Tested native functionality vs in-browser fallbacks.
- [x] RemUI vs native app boundary clearly defined in one paragraph.
- [x] Evidence screenshots collected for native activities, fallbacks, and RemUI boundary.

---

## PASS ✅
