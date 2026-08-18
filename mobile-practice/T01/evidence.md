# T01 — Install the App Development Environment

**Date:** 2026-08-17
**Branch:** client/bdata-lms
**Tag:** v5.2.1

## git remote -v output
origin   https://github.com/bdata-lab/moodleapp.git (fetch)
origin   https://github.com/bdata-lab/moodleapp.git (push)
upstream https://github.com/moodlehq/moodleapp.git (fetch)
upstream https://github.com/moodlehq/moodleapp.git (push)

## Environment
- Node: v22.23.2
- npm: 10.9.8
- OS: Windows 11
- Branch: client/bdata-lms (from tag v5.2.1)

## npm start
- Used: npm run start:win (Windows — no SSL)
- URL: http://localhost:8100
- Result: Compiled successfully

## Pass Criteria
- [x] origin = bdata-lab/moodleapp
- [x] upstream = moodlehq/moodleapp
- [x] App UI loads in browser without compile errors
- [x] Branch from stable tag (v5.2.1)
- [x] Not on main branch

## Notes
- npm start (--ssl) causes ERR_SSL_PROTOCOL_ERROR on Windows
- Use: npm run start:win for Windows development
- Browser build shows LMS connection error (expected — CORS in browser mode)
- Real device testing needed for LMS login (T05)

## PASS ✅
