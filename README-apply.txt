My Cash: Tracker - GitHub replacement files

IMPORTANT: This is a patch package, not a full Android project. Copy/replace only the listed files in your existing repository.

1) Replace:
   masrofaty-android/www/index.html
   with the file at the same path in this ZIP.

2) Replace:
   masrofaty-android/capacitor.config.json
   with the file at the same path in this ZIP.
   The appId is intentionally kept as com.yourname.masrofaty so an installed build can retain the same Android package identity. Only the visible app name changes.

3) Replace:
   masrofaty-android/package.json
   with the file at the same path in this ZIP.
   This adds @capacitor/local-notifications, which the HTML checks for native Android notifications.

4) The ZIP file named .github-workflow-build-apk.yml is intended to replace:
   .github/workflows/build-apk.yml
   Rename it to build-apk.yml and upload it to that exact path.

5) Keep the existing android-debug.keystore and other Android project files for now. Do not upload any release signing key or passwords to a public repository.

6) After committing these changes, open the repository's Actions tab, select "Build Android APK", and run it (or wait for the push-triggered build). Download the APK from the successful run's Artifacts section.

Notes:
- index.html contains the PingAR font embedded in the HTML, so it does not depend on a separate font path.
- This package does not contain the generated Android project and does not guarantee a successful build until GitHub Actions runs.
- The HTML has an optional notification permission prompt, but Android notifications only work if the Capacitor Local Notifications plugin is synced into the Android project and the app's reminder code schedules notifications.
