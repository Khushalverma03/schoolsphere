# SchoolSphere Android MVP source

Flutter source for a school-management Android MVP. Includes an overview dashboard, student list/search/add flow, simulated entry/exit events, fee and marks placeholder screens, and a configurable backend URL.

## APK build status

An APK has **not** been compiled in this environment: Flutter and Android SDK/build tools are absent, and this runtime cannot reach the internet to install them. I have added a GitHub Actions workflow so GitHub's build runner can compile the APK for you without installing Android tools on your computer.

## Build APK using GitHub Actions

1. Create a new repository on GitHub.
2. Upload/push the contents of this folder to that repository (the `.github/workflows/build-apk.yml` file must be included).
3. Open the repository's **Actions** tab.
4. Select **Build SchoolSphere Android APK** and click **Run workflow** (or push to `main`/`master`).
5. When the workflow finishes successfully, open its run and download the `schoolsphere-debug-apk` artifact.
6. Extract the artifact ZIP; it contains `app-debug.apk`. Transfer it to your Android phone and install it, allowing installs from that source if Android asks.

The workflow generates the Android platform files, resolves Flutter dependencies, builds a debug APK, and uploads it as a downloadable artifact. GitHub account/repository access is needed to run this remote build.

## Local build (if Flutter is installed)

```bash
flutter create . --platforms=android
flutter pub get
flutter build apk --debug
```

Output: `build/app/outputs/flutter-apk/app-debug.apk`

## Backend connection

The default URL is `http://10.0.2.2:8080/api`, the host-machine alias for the Android emulator. On a physical phone, change the URL in app Settings to `http://YOUR_COMPUTER_LAN_IP:8080/api`; both devices must share a network and the computer firewall must allow the connection.

## Limitations and safety

- The app uses sample data when the API is unavailable. Demo-only student additions and simulated attendance events are not saved permanently.
- This is a development preview, not production-ready software.
- No login, authorization, school tenant isolation, production privacy/security controls, payment integration, or real biometric-device integration yet.
- The workflow enables cleartext HTTP for local development. Do not use that setting for a public production release; use HTTPS and production-grade security.
- Use synthetic test data only. Do not enter real student, guardian, financial, or biometric information into this MVP.
