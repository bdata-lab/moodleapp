# Moodle App Upgrade Checklist (Runbook)

**1. Check Current State**
* Check and note the current Moodle HQ tag our `client/bdata` branch is based on (e.g., `v4.3.0`).

**2. Fetch Upstream & Review**
* Run `git fetch upstream --tags` to get the latest releases from Moodle HQ.
* Read the Moodle HQ release notes for the target tag to identify any breaking changes or plugin deprecations.

**3. Files to Re-apply / Verify after Merge**
To ensure our custom branding is not destroyed by the upstream update, these specific files must be preserved or re-applied:
* `moodle.config.json` (Custom site URL, App IDs, and forced URL schemes)
* Custom SCSS files (e.g., `src/theme/variables.scss` for BDATA colors)
* `resources/` directory (Custom app icons and splash screens)
* `package.json` & `config.xml` (Custom bundle IDs and version codes)

**4. Throwaway Branch Drill**
* Create a test branch: `git checkout -b drill-upgrade-test`
* Merge the new upstream tag: `git merge <new-upstream-tag>`
* Resolve merge conflicts (prioritizing our custom files listed in step 3).
* Build the app to confirm successful compilation and push to test environment.

**5. Fast-Forward Strategy for Main Branch**
* Should `main` (or our client branch) on `bdata-lab` fast-forward?
* **Answer: NO.** Because we have made custom commits (branding, configuration) on top of the original upstream code, a simple fast-forward is impossible. We must use a **merge commit** (or carefully rebase our custom commits on top of the new tag) to maintain our custom application logic.
