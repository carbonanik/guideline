# Flutter Internals & Architecture

To reach a senior level, you must understand what happens "under the hood."

## 1. The Three Layers

### Framework (Dart)
The part developers interact with mostly. It includes:
- **Material / Cupertino:** High-level UI components.
- **Widgets:** The building blocks.
- **Rendering:** Handles layout and painting.
- **Animation, Painting, Gestures:** Core low-level services.

### Engine (C/C++)
The core of Flutter. It provides the low-level implementation of Flutter's core API.
- **Graphics (Skia/Impeller):** Most important part. Handles the actual drawing.
- **Text Layout:** Positioning and rendering text.
- **File & Network I/O:** Core platform services.
- **Dart Runtime:** Managing the lifecycle of Dart code.

### Embedder (Platform Specific)
The layer that allows Flutter to run on any OS (Android, iOS, Web, Windows).
- Handles packaging, input (touch, mouse), and message passing.

## 2. Rendering: How UI appears
Flutter doesn't use native OEM widgets (like Android's `Button` or iOS's `UIButton`). Instead, it paints every pixel itself.

| Feature | OEM Widgets (Native) | Flutter (Skia/Impeller) |
| --- | --- | --- |
| **Rendering** | OS Handles it | Flutter Engine Handles it |
| **Consistency** | Varies by OS version | Identical across all versions |
| **Performance** | Can be slow (IPC) | Extremely fast (Direct GPU) |

## 3. Why is Flutter Fast?
1. **No Bridge:** Unlike React Native, there is no JavaScript-to-Native bridge. Dart is compiled ahead-of-time (AOT) to machine code.
2. **Efficient Rendering:** It bypasses the platform's widget sets and draws directly to a canvas.
3. **Sub-linear Layout:** Flutter's layout algorithm is $O(N)$, meaning it only visits each node once.

---
**Next Sitting Recommendation:** [Flutter Fundamentals](https://github.com/carbonanik/guideline/blob/master/interview_prep/flutter_fundamentals.md) to see how these layers manifest in widgets.
