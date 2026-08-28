# Production Cutover & Rollback Runbook

1. **Change URL:** Open `moodle.config.json` and update `siteurl` from staging to the production URL.
2. **Bump Version:** Open `package.json` (or `config.xml`) and bump the `version` (e.g., 1.0.0 to 1.0.1) and `versionCode` (e.g., 1 to 2).
3. **Apply Changes:** Run the app setup script (e.g., `npm run setup` or `npm run build`) to apply the new config.
4. **Rebuild:** Generate the new signed release APK/AAB using Android Studio or current build script.
5. **Verify:** Install the new APK on a device and confirm successful login to the production site.
6. **Rollback (Step 1):** If production login fails, uninstall the broken app from the device immediately.
7. **Rollback (Step 2):** Reinstall the previous known-good Staging APK (from T13) / TestFlight build.
8. **Rollback (Step 3):** Revert changes in `moodle.config.json` and `package.json` via `git checkout`.
