# T16 — Custom-App Push (Implementation & Residual-Risk Report)

**Date:** 2026-08-25  
**Branch:** `client/bdata-lms`  
**Application ID:** `com.bdata.moodleapp`  
**Target Staging:** `https://moodle.bdata.com.mm`  

---

## 1. Documentation

Because push notifications for the custom branded Application ID (`com.bdata.moodleapp`) require a dedicated private Airnotifier server and Firebase Cloud Messaging credentials, technical findings and infrastructure requirements are documented in the **Residual-Risk Report**:

👉 **[T16 Push Notification Residual-Risk Report](./residual-risk-report.md)**

---

## 2. Artifacts

- [`residual-risk-report.md`](./residual-risk-report.md) — Comprehensive technical report detailing push architecture, failure mode (token rejection), infrastructure blockers, and next steps for deployment.
