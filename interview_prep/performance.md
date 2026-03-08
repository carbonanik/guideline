# Performance & Rendering Pipeline

## 1. The Rendering Pipeline
Every frame goes through these stages:
1. **Build:** Widgets are created/re-created.
2. **Layout:** Calculating the size and position of every `RenderObject`. Constraints go DOWN, Sizes go UP.
3. **Paint:** Recording painting commands (e.g., `drawLine`, `drawRect`).
4. **Compositing:** Sending the recorded layers to the GPU to be combined and displayed.

## 2. Optimization Techniques

### Minimize Rebuilds
- **Use `const` constructors:** Allows Flutter to skip building that widget entirely if its parameters haven't changed.
- **Localized Rebuilds:** Use `ValueListenableBuilder` or `Consumer` (Riverpod) to rebuild only the small part of the UI that changed.
- **Avoid calling `setState` at the root:** Keep state as low as possible in the tree.

### RepaintBoundary
- If you have a complex animation in one part of the screen, it might trigger repaints for the whole screen.
- Wrap the expensive/moving part in a `RepaintBoundary` to create a separate "layer" for it.

### List Optimizations
- Always use `ListView.builder` for long lists (lazy loading).
- Provide an `itemExtent` if items have a fixed height to avoid layout calculations.

## 3. Keys in Flutter
Keys are vital for preserving state when widgets move in the tree.

- **ValueKey:** For simple items (e.g., a list item with a unique ID).
- **ObjectKey:** For items identified by a complex object.
- **UniqueKey:** Forces a new element/state every time (rarely used).
- **GlobalKey:** Accesses the state of a widget from anywhere. **Use sparingly** as it is expensive.

### Question: "When should I use a Key?"
**Answer:** Use keys when you have a **Stateful** widget collection that changes order or filters. Without keys, Flutter might associate the old state with the new widget at the same position.

---
**Next Sitting Recommendation:** [State Management](file:///home/carbonanik/code/guideline/interview_prep/state_management.md) to learn how to trigger these optimizations.
