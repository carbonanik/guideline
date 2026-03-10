# Flutter Fundamentals, Widgets, and Lifecycle

## 1. Widget Types
- **StatelessWidget:** Immutable. It doesn't change its state during its lifetime.
- **StatefulWidget:** Mutable. It can change its state and trigger a rebuild of the UI.
- **InheritedWidget:** Used for passing data down the widget tree efficiently. Basis for `Provider`.

## 2. The Three Trees (Deep Dive)
Senior developers must explain the relationship between these trees:

1. **Widget Tree:** 
   - Immutable blueprints. 
   - Recreated frequently (cheap).
2. **Element Tree:** 
   - The "Glue" or "Manager." 
   - Mutable objects that maintain the lifecycle. 
   - Elements reference both their Widget and their RenderObject.
3. **RenderObject Tree:** 
   - Handles the actual geometry, layout, and painting. 
   - Expensive to create; Flutter tries to reuse them as much as possible by only updating properties.

### Key Interview Question: "Why does Flutter have three trees?"
**Answer:** Separation of concerns. Widgets are for configuration, Elements for lifecycle management, and RenderObjects for expensive painting. This separation allows Flutter to perform "diffing" at the Element level and only repaint what's necessary.

### "Why are rebuilds fast?"
Widgets are just lightweight, immutable **Configuration Objects**. Rebuilding a widget tree doesn't rebuild the actual UI; it just creates new blueprints. Flutter’s Element tree then performs "smart diffing" to reuse existing RenderObjects, minimizing expensive layout and paint operations.

## 3. Widget Lifecycle (Stateful)
1. **`createState()`:** Called first to create the state object.
2. **`initState()`:** Initial setup (e.g., controllers, listeners). Called once.
3. **`didChangeDependencies()`:** Called after `initState` and when an `InheritedWidget` it depends on changes.
4. **`build()`:** Returns the widget tree. 
   - **Crucial Rule:** The `build` method must be **Pure**. It should not trigger side effects (API calls, data mutations) as it can be called many times per second.
5. **`didUpdateWidget()`:** Called when the parent widget changes properties that require a rebuild.
6. **`dispose()`:** Final cleanup (cancel timers, listeners, controllers).

## 4. `setState()` Internals
When you call `setState()`:
1. The `Element` is marked as **dirty** via `markNeedsBuild()`.
2. Flutter schedules a frame via `SchedulerBinding`.
3. During the **Build** phase, the `BuildOwner` rebuilds only the dirty subtrees.
4. The pipeline continues: Layout → Paint → Compositing → Rasterization.

## 5. Key Concepts
- **Key:** Used to identify a widget and preserve state during tree changes (e.g., `ValueKey`, `UniqueKey`, `GlobalKey`).
- **BuildContext:** A handle to the **Element** in the tree. It represents the location of a widget and provides access to parent information (e.g., `Theme.of(context)`).

---
**Next Sitting Recommendation:** [Performance & Pipeline](./performance.md) to understand how to optimize your builds.
