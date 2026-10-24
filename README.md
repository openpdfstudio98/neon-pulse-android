# Neon Pulse Ultimate V3 — Android Cloud Build Ready

This is a **Capacitor Android project with a Codemagic CI workflow**. It generates a **debug APK** in the cloud; no PC or Android Studio is needed to trigger the build. **An APK is not included in this ZIP.**

## Phone-only setup (GitHub + Codemagic)

1. Extract the ZIP using your Android phone's Files app. The files `codemagic.yaml`, `package.json`, `capacitor.config.json`, and the folder `www` must be at the **root** of the GitHub repository.
2. In your phone browser, visit https://github.com/new and create a **private** repository (e.g. `neon-pulse-android`).
3. Open the repository, choose **Add file > Upload files** (use **Desktop site** in your browser if the button is hidden). Upload the **contents of the extracted folder**, preserving `www/index.html`. If mobile GitHub cannot upload a folder, use a GitHub-capable file manager or a web IDE to create the `www` folder and upload `index.html` inside it. Do **not** upload the ZIP as a single file and expect the build to work.
4. Go to https://codemagic.io/start/ and sign in with GitHub. Authorize access to the repository.
5. Add the repository as an application. Select **Codemagic YAML** workflow configuration, and select the `android-debug` workflow.
6. Press **Start new build**. Codemagic installs Node dependencies, generates the Android project, and builds a debug APK. The first build may take several minutes.
7. After a successful build, open its **Artifacts** section and download the `app-debug.apk` to your Android phone. Install it only if you trust the source. Android may ask permission to install from your browser/files app.
8. Launch and test touch controls, gameplay, shop, rewards, pause/resume and app backgrounding. Report any error with a screenshot of the Codemagic build log.

## Notes and limitations

- This workflow builds a **debug APK for testing**, not a signed release AAB for the Play Store.
- The build requires a Codemagic account and its available build minutes; plan quotas and availability can change.
- The current HTML imports **Tailwind CSS, Font Awesome, Google Fonts and Firebase from online CDNs**. The game is **not fully offline-ready** and first launch may require an internet connection. Some UI can fail without connectivity.
- Google Play Games Services **is not integrated**. Login, real Play Games leaderboard, and Play achievements require Play Console IDs, Android native SDK/bridge and signed testing builds.
- The existing game may display simulated rivals in its **local** leaderboard. Do not confuse them with real Google Play Games scores.
- The `com.neonpulse.orbitdash` application ID is a starting value. Confirm ownership and uniqueness before publication.
- Debug builds are not suitable for release. Protect your release signing keys when moving to AAB production builds.
- Codemagic's available build machines and Android SDK versions can change. If the build fails due to a toolchain mismatch, inspect the logs and adjust the YAML accordingly.

## File layout

```
/codemagic.yaml
/package.json
/capacitor.config.json
/.gitignore
/www/index.html
/README.md
```

## Later: Google Play Games Services

1. Set up Play Console (adult account owner required), Android game entry and Play Games Services project.
2. Set up OAuth / SHA-1 certificate fingerprints and tester accounts.
3. Implement a native Capacitor bridge to Play Games Services SDK for login, leaderboard and achievements.
4. Configure cloud save separately if desired, and replace simulated rivals with an explicitly labeled local leaderboard.
5. Generate a properly signed release AAB and test it before submitting to Play Store.
