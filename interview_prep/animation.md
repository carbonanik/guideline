# Animation (VSync & Core Concepts)

## VSync (Vertical Synchronization)
VSync is a signaling mechanism used by the display hardware to notify the operating system (and Flutter) that it's ready to refresh the screen, typically at 60Hz or 120Hz.

### Why it matters:
- **Prevents Tearing:** Ensures the graphics hardware doesn't update the screen while it's mid-refresh.
- **Efficiency:** Flutter only builds and paints when a VSync signal is received, preventing unnecessary work.
- **Smoothness:** Syncing with the hardware refresh rate ensures consistent frame delivery.

## Core Animation Classes

### 1. Ticker
- A `Ticker` is an object that sends a signal for every frame of the animation.
- In Flutter, `SingleTickerProviderStateMixin` is used in `StatefulWidget` to provide a `Ticker`.

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
