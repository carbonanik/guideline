# CI/CD & DevOps for Flutter

A senior developer ensures that the path from code to production is automated, reliable, and reproducible.

## 1. Automation with Fastlane

**Fastlane** is the industry standard for automating screenshots, managing provisioning profiles, and releasing apps.

- **Fastfile:** Defines "lanes" (e.g., `lane :beta` or `lane :deploy`).
- **Appfile:** Stores identifiers (Bundle ID, Team ID).
- **Match:** Used to sync certificates and profiles across the team.

## 2. CI/CD Pipelines (GitHub Actions / Codemagic)

How do you automate testing and building?

- **Lint Check:** `flutter analyze`.
- **Unit Tests:** `flutter test`.
- **Build:** `flutter build apk --release` / `flutter build ios --no-codesign`.
- **Deploy:** Upload to Firebase App Distribution or Play Store Internal Track.

## 3. Shorebird (Code Push)

One of the newest and most "Senior" topics in Flutter.

- **Problem:** Fixing a small bug requires a full store review (days).
- **Solution:** **Shorebird**. It allows you to push code updates directly to the user's device without a store update (Android only, iOS support in progress).
- **Caveat:** You cannot change native code or assets via code push.

## 4. Deployment Strategies

### Blue-Green vs. Canary
- **Canary:** Release the update to 5% of users first. Monitor crash rates (Sentry/Firebase). If stable, rollout to 100%.

### Feature Flags
- Use tools like **Firebase Remote Config** or **LaunchDarkly** to toggle features on/off without a new build.

## 5. Production Monitoring
- **Crash Reporting:** Firebase Crashlytics or Sentry. Track "Fatal" vs "Non-fatal" errors.
- **Analytics:** Firebase Analytics to track user behavior and feature adoption.
- **Log Management:** Use a structured logging approach to debug production issues efficiently.

## 5. Senior Scenario
- **Question:** "Our build takes 30 minutes. How do you speed it up?"
- **Answer:**
  - Cache the Flutter SDK and Pub cache in the CI environment.
  - Use modularized packages (only test what changed).
  - Use a higher-performance runner (e.g., M1 Mac runners for iOS).

---
**Next Sitting Recommendation:** [Senior Thinking](./senior_thinking.md) to wrap up the technical preparation.
