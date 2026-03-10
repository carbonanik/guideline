# Animation (VSync & Core Concepts)

## VSync (Vertical Synchronization)
VSync is the mechanism used to synchronize the timing of animations and visual updates with the device's display refresh rate (typically 60Hz or 120Hz).

### Why it matters:
- **Prevents Tearing:** Ensures only complete frames are displayed by waiting for the signal that the screen is ready.
- **Smoothness:** Aligns the app's frame rate with the hardware refresh rate for stutter-free delivery.
- **Resource Efficiency:** Conserves system resources by pausing animations when the widget is not visible.

### How it works in Flutter
1. **The Signal:** A VSync signal tells Flutter exactly when to draw a new frame.
2. **The Ticker:** The `Ticker` class generates a stream of frames synchronized with this signal.
3. **TickerProvider:** Acting as the "binding agent," the `TickerProvider` links the `Ticker` to the Flutter framework.

## Implementation: Using VSync in Code
To use VSync in a `StatefulWidget`, you must apply a mixin to provide the `TickerProvider`:

- **SingleTickerProviderStateMixin:** Use when you only need **one** `AnimationController`.
- **TickerProviderStateMixin:** Use when you need **multiple** `AnimationControllers`.

### Example
```dart
class MyStatefulWidgetState extends State<MyStatefulWidget> 
    with SingleTickerProviderStateMixin { // 1. Apply the mixin
  late AnimationController _controller;

  @override
  void initState() {
    super.initState();
    _controller = AnimationController(
      duration: const Duration(seconds: 2),
      vsync: this, // 2. Pass 'this' as the TickerProvider
    );
  }

  @override
  void dispose() {
    _controller.dispose(); // Always dispose!
    super.dispose();
  }
  // ... build method
}
```

## Core Animation Classes

### 1. Ticker
- A class that calls a callback once per frame (~60-120 times per second) while active.
- **Synced Efficiency:** Unlike a standard `Timer.periodic`, a `Ticker` only ticks when the screen is ready for a redraw, saving battery and preventing jitter.
- Ticker provides the **elapsed time**, which the `AnimationController` uses to calculate the animation's current progress (0.0 to 1.0).

### 2. AnimationController
- Manages the animation state (forward, reverse, stop).
- Links a `Ticker` to the animation.
- Defines the `duration` and range (usually 0.0 to 1.0).

### 3. Tween (Between)
- Maps the 0.0-1.0 range of the controller to a different range of values (e.g., `Color`, `Size`, `Offset`).
- Example: `Tween<double>(begin: 0, end: 100).animate(controller);`

## Implicit vs. Explicit Animations

| Feature | Implicit Animations | Explicit Animations |
| --- | --- | --- |
| **Complexity** | Simple | More Control |
| **Widgets** | `AnimatedContainer`, `AnimatedOpacity` | `RotationTransition`, `ScaleTransition` |
| **Controller** | Managed by Flutter | Managed by Developer |
| **Scenario** | Simple transitions | Complex, repeating, or manual control |

## Performance Tips
- Use `RepaintBoundary` to isolate expensive painting.
- Minimize work in the `build` method during animations.
- Use `SizedBox` or `const` widgets inside animations where possible.
