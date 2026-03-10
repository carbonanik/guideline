# Security Deep Dive

Senior developers must prioritize user data protection and app integrity. Security isn't just about logic; it's about protecting against reverse engineering and man-in-the-middle (MITM) attacks.

## 1. Data at Rest (Local Storage)

How do you store sensitive information like API tokens or user credentials?

| Method | Security Level | Best For |
| --- | --- | --- |
| `shared_preferences` | **Low** | Non-sensitive UI settings. |
| `flutter_secure_storage` | **High** | Auth tokens, credentials (uses Keychain/Keystore). |
| `hive` (with encryption) | **Medium** | Large amounts of data that need encryption. |

> [!WARNING]
> Never store plain-text passwords or credit card numbers, even in "secure" storage. Use tokens provided by your backend or payment provider.

## 2. Data in Transit (Network Security)

### SSL Pinning
- **Scenario:** An attacker uses a proxy (like Charles or Proxyman) to read your API traffic.
- **Solution:** **SSL Pinning**. The app is hardcoded to only trust a specific certificate or public key from your server.
- **Implementation:** Use `dio_http2_adapter` or custom `SecurityContext` in `HttpClient` to provide the trusted certificate.

## 3. App Integrity & Reverse Engineering

### Obfuscation
- **Why?** JavaScript and Dart can be decompiled into readable code.
- **Solution:** Use `--obfuscate` and `--split-debug-info` when building.
- **Senior Tip:** Mention that this doesn't make the app "unhackable," but much harder to read.

### Root & Jailbreak Detection
- **Scenario:** The app should not run on compromised devices to prevent tampering.
- **Solution:** Use plugins like `flutter_jailbreak_detection` or `free_rasp` to check for root access or attached debuggers.

## 4. Security Checklist
- [ ] No hardcoded API keys in the source code (use `--dart-define`).
- [ ] Enable ProGuard/R8 for Android.
- [ ] Implement Certificate Pinning for critical APIs.
- [ ] Use `flutter_secure_storage` for all sensitive tokens.

---
**Next Sitting Recommendation:** [CI/CD & DevOps](./devops_cicd.md) to automate security checks in the pipeline.
