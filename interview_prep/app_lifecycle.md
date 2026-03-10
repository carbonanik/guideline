# App Lifecycle In-Depth

Understanding the lifecycle is crucial for resource management (camera, location), analytics, and saving user state.

## 1. AppLifecycleState Enum

Flutter maps native lifecycle events to the `AppLifecycleState` enum.

| State | Description | Trigger Example |
| --- | --- | --- |
| **resumed** | App is visible and responding to user input. | App launched or returned to. |
| **inactive** | App is in an idle state; not receiving input. | Phone call receipt, system dialog. |
| **hidden** | (Flutter 3.13+) App is hidden but not paused. | Transitioning between foreground/background. |
| **paused** | App is in the background; not visible to user. | Home button pressed. |
| **detached** | App is still hosted but detached from any views. | App is being terminated. |

## 2. Using WidgetsBindingObserver

To listen to lifecycle changes, you must use the `WidgetsBindingObserver` mixin.

```dart
class MyLifecycleManager extends StatefulWidget {
  @override
  _MyLifecycleManagerState createState() => _MyLifecycleManagerState();
}

class _MyLifecycleManagerState extends State<MyLifecycleManager> with WidgetsBindingObserver {
  @override
  void initState() {
    super.initState();
    WidgetsBinding.instance.addObserver(this);
  }

  @override
  void dispose() {
    WidgetsBinding.instance.removeObserver(this);
    super.dispose();
  }

  @override
  void didChangeAppLifecycleState(AppLifecycleState state) {
    print("New State: $state");
    if (state == AppLifecycleState.paused) {
      // Save data, stop camera, stop location
    } else if (state == AppLifecycleState.resumed) {
      // Restart services
    }
  }
}
```

## 3. Native Lifecycle Mapping

| Flutter State | Android Activity State | iOS App State |
| --- | --- | --- |
| `resumed` | `onResume()` | `applicationDidBecomeActive` |
| `inactive` | `onPause()` | `applicationWillResignActive` |
| `paused` | `onStop()` | `applicationDidEnterBackground` |
| `detached` | `onDestroy()` | `applicationWillTerminate` |

## 4. Senior Scenario: State Restoration

If the OS kills your app in the background to reclaim memory, the user expects to return to the exact same scroll position or text input.

- **Problem:** Normal state is lost on process death.
- **Solution:** `RestorationManager` and `RestorationMixin`.
- Use `RestorableProperty` (e.g., `RestorableInt`, `RestorableTextEditingController`) to tell the OS what data to preserve.

## 5. Background Processing

Flutter can run code when the app is NOT in the foreground using **Isolates** and **WorkManager** (Android) or **Background Fetch** (iOS).
- Common use case: Periodic data sync, Geofencing.
- **Limitation:** Background execution is limited by the OS (Battery optimization).

---
> [!IMPORTANT]
> **Senior Tip:** Don't just say "I use `inactive` for phone calls." Explain that `inactive` is the gateway between foreground and background. On iOS, a swipe-down of the Control Center triggers `inactive`, while on Android, it might not. Always test behavior on both platforms.

**Next Sitting Recommendation:** [Security Deep Dive](./security.md) to understand how to protect user data and app integrity.
