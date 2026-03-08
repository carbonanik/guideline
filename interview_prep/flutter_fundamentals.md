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

## 3. Widget Lifecycle (Stateful)
1. **`createState()`:** Called first to create the state object.
2. **`initState()`:** Initial setup (e.g., controllers, listeners). Called once.
3. **`didChangeDependencies()`:** Called after `initState` and when an `InheritedWidget` it depends on changes.
4. **`build()`:** Returns the widget tree. 
   - **Crucial Rule:** The `build` method must be **Pure**. It should not trigger side effects (API calls, data mutations) as it can be called many times per second.
5. **`didUpdateWidget()`:** Called when the parent widget changes properties that require a rebuild.
6. **`dispose()`:** Final cleanup (cancel timers, listeners, controllers).

## 5. Key Concepts
- **Key:** Used to identify a widget and preserve state during tree changes (e.g., `ValueKey`, `UniqueKey`, `GlobalKey`).
- **BuildContext:** An object that provides information about the widget's location in the tree.
