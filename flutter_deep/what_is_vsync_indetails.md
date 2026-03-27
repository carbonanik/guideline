Viewed binding.dart:1-800

In the context of computer graphics and Flutter, **VSYNC** (Vertical Synchronization) is the "heartbeat" of your UI.

Here is a deep technical breakdown of what it is and how Flutter uses it.

---

### 1. The Physical Problem: "Tearing"
To understand VSync, you must understand the hardware. A phone screen doesn't "glow" all at once; it updates pixels line-by-line from top to bottom.
*   **The Scan**: The display hardware reads from a memory buffer (the **Front Buffer**) and sends that data to the screen.
*   **The Conflict**: If the GPU updates the Front Buffer *while* the screen is mid-scan, the top half of the screen will show the old frame, and the bottom half will show the new frame. This visual glitch is called **Tearing**.

### 2. The Solution: Double Buffering & VSync
To prevent tearing, systems use **Double Buffering**:
1.  **Front Buffer**: The screen is currently reading from this.
2.  **Back Buffer**: The GPU is "drawing" the next frame here.
3.  **VSYNC Signal**: When the screen finishes drawing the last pixel at the bottom, it sends a hardware interrupt called the **Vertical Synchronization pulse**.
4.  **The Swap**: Only when the VSync pulse happens, the system "swaps" the buffers. The Back Buffer becomes the Front Buffer, and the cycle repeats.

---

### 3. How Flutter Hooks into VSync
Flutter is a **VSync-driven framework**. It does absolutely nothing until it receives a signal from the operating system.

#### The Chain of Events:
1.  **Hardware Impulse**: The screen sends a VSync signal to the Android/iOS kernel.
2.  **Engine Latency**: The Flutter Engine (C++) receives this signal via the [VsyncWaiter](cci:1://file:///home/carbonanik/code/flutter/engine/src/flutter/shell/common/shell.cc:2456:0-2461:1).
3.  **Dart Callback**: The Engine triggers the `platformDispatcher.onBeginFrame` callback in Dart.
4.  **Framework Execution**:
    *   **[handleBeginFrame](cci:1://file:///home/carbonanik/code/flutter/packages/flutter/lib/src/scheduler/binding.dart:1202:2-1273:3)**: Runs Animations and Tickers.
    *   **[handleDrawFrame](cci:1://file:///home/carbonanik/code/flutter/packages/flutter/lib/src/scheduler/binding.dart:1328:2-1375:3)**: Runs the Build, Layout, and Paint phases.
5.  **The Submission**: The resulting "Layer Tree" is sent back to the Engine, which then tells the GPU to rasterize it so it's ready for the **next** VSync swap.

### 4. The "Frame Budget" (The Math)
VSync defines your time limit. If you miss the budget, you get **Jank** (dropped frames).

| Refresh Rate | VSync Interval | Your Total Budget |
| :--- | :--- | :--- |
| **60 Hz** | ~16.67 ms | 16.6 ms to do Build + Layout + Paint + GPU work |
| **90 Hz** | ~11.11 ms | 11.1 ms |
| **120 Hz** | ~8.33 ms | 8.3 ms |

If your Dart code takes **17ms** on a 60Hz screen, the system misses the VSync pulse. The screen has to show the **old frame** for another cycle. This is what users perceive as a "stutter."

### 5. Advanced: Variable Refresh Rate (VRR)
Modern high-end phones (like iPhone's ProMotion or Android LTPO screens) use **Adaptive VSync**. 
*   If the screen is static, the VSync pulse might only happen **1 time per second** (1Hz) to save battery.
*   The moment you touch the screen, the Engine requests the OS to ramp the VSync pulses up to **120Hz**.

### Summary
**VSync is the conductor of the orchestra.** It ensures that the GPU and the Display are perfectly synchronized so that the user sees a smooth, tear-free image exactly when the hardware is ready to show it.