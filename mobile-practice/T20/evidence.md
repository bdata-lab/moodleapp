# T20 — Go-Live Rehearsal (Staging → Production Cutover & Rollback)

**Date:** 2026-08-28  
**Branch:** `client/bdata-lms`  
**Tag:** `v5.2.1`  

---

## 1. Objective

Document the concise, 10-line production cutover and emergency rollback runbook for switching from staging to production URL and performing version bumping without breaking authentication.

---

## 2. Deliverables

- Primary document: [`runbook.md`](./runbook.md)

---

## 3. Pass Criteria

- [x] Clear cutover sequence documented (URL update, version bump, rebuild, verify).
- [x] Emergency rollback steps defined (uninstall, restore previous known-good build, git revert).
- [x] Concise format under 10 lines.

---

## PASS ✅
