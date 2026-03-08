# Native Communication (Platform Channels)

Sometimes Flutter needs to talk to the underlying OS (Android/iOS) to access features not available in Dart (e.g., specialized sensors, legacy native SDKs).

## 1. How it works
Flutter uses **Message Passing** (Binary Messenger). It’s asynchronous.

### MethodChannel
The most common way to communicate.
- **Flutter side:** Invokes a method by name.
- **Native side:** Listens for that name and executes Java/Kotlin/Swift/Obj-C code.

## 2. Platform Channel Types

| Type | Purpose |
| --- | --- |
| **MethodChannel** | Request-Response (Trigger a native action and get a result). |
| **EventChannel** | Stream-based (Listen to native events like sensor data). |
| **BasicMessageChannel** | Sending string/binary data continuously. |

## 3. Code Example (Mental Model)
**Flutter:**
```dart
static const platform = MethodChannel('com.example.app/battery');
final int result = await platform.invokeMethod('getBatteryLevel');
```

**Android (Kotlin):**
```kotlin
MethodChannel(flutterEngine.dartExecutor.binaryMessenger, CHANNEL).setMethodCallHandler { call, result ->
  if (call.method == "getBatteryLevel") {
    result.success(getBatteryLevel())
  }
}
```

## 4. Federated Plugins
A modern way to structure plugins where different packages handle different platforms (Web, Android, iOS), all sharing a common interface.

### Question: "Are Platform Channels synchronous?"
**Answer:** No. Communication across the "bridge" is always asynchronous, even if the native code itself is synchronous.

---
**Next Sitting Recommendation:** [Senior Thinking](file:///home/carbonanik/code/guideline/interview_prep/senior_thinking.md)
