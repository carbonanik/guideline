# Flutter DevTools Mastery

To build high-performance apps, you must master the tools provided by the Flutter team for debugging and profiling.

## 1. Widget Inspector
Used for debugging UI layouts and identifying unnecessary rebuilds.
- **Select Widget Mode:** Inspect specific widgets on the screen.
- **Highlight Repaints:** Visualizes what parts of the screen are being repainted (helps identify if a `RepaintBoundary` is needed).
- **Rebuild Stats:** Tracks how many times each widget has rebuilt.

## 2. Performance Profiler
Identifying "Jank" (dropped frames).
- **Frames Chart:** Shows the time spent on the **UI Thread** vs. **Raster Thread**.
- **Jank Detection:** If a frame takes longer than 16ms (for 60fps), it shows as a red bar.
- **Enhancement:** Use `Timeline.startSync` and `Timeline.finishSync` to add custom events to the profiler.

## 3. Memory Profiler
Detecting memory leaks and excessive heap usage.
- **Heap Snapshot:** Shows all objects currently in memory.
- **Leak Detection:** Identifying objects that remain in memory after they should have been garbage collected (e.g., forgotten `StreamController` or `AnimationController`).
- **Image Tracking:** Large images are the most common cause of high memory usage. Ensure images are resized before being loaded into memory.

## 4. CPU Profiler
Finding bottlenecks in your logic.
- **Call Tree:** Shows which functions are consuming the most CPU time.
- **Flame Chart:** A visual representation of function execution over time.
- **Senior Move:** Identify CPU-intensive tasks and move them to an **Isolate** to keep the UI thread smooth.

## 5. Network Profiler
Monitoring API traffic.
- View requests, responses, headers, and payload size.
- Useful for debugging authentication flows (token headers) and payload optimization.

---

### [!IMPORTANT]
### How to Profile Correctly
Never measure performance in **Debug Mode**. Always use **Profile Mode** (`flutter run --profile`). Debug mode has extra check overhead (like `asserts`) that makes performance look much worse than it actually is.

---
**Next Sitting Recommendation:** [Testing Strategies](./testing.md) to ensure your high-performance code remains stable.
