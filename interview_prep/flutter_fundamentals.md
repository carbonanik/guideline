# Flutter Fundamentals, Widgets, and Lifecycle

## 1. Widget Types
- **StatelessWidget:** Immutable. It doesn't change its state during its lifetime.
- **StatefulWidget:** Mutable. It can change its state and trigger a rebuild of the UI.
- **InheritedWidget:** Used for passing data down the widget tree efficiently. Basis for `Provider`.

## 2. Widget Lifecycle (Stateful)
1. **`createState()`:** Called first to create the state object.
2. **`initState()`:** Initial setup (e.g., controllers, listeners). Called once.
3. **`didChangeDependencies()`:** Called after `initState` and when an `InheritedWidget` it depends on changes.
4. **`build()`:** Returns the widget tree. Called frequently.
5. **`didUpdateWidget()`:** Called when the parent widget changes properties that require a rebuild.
6. **`dispose()`:** Final cleanup (cancel timers, listeners, controllers).

## 3. App Lifecycle
Use `WidgetsBindingObserver` to listen to app state changes:
- `resumed`: App is in focus and visible.
- `inactive`: App is in a transitional state (e.g., phone call incoming).
- `paused`: App is in the background.
- `detached`: App is about to be terminated.

## 4. The Three Trees
- **Widget Tree:** A blueprint of what the UI should look like.
- **Element Tree:** Manages the lifecycle and location of widgets in the tree. Bridges Widget and RenderObject.
- **RenderObject Tree:** Handles the actual layout and painting on the screen.

## 5. Key Concepts
- **Key:** Used to identify a widget and preserve state during tree changes (e.g., `ValueKey`, `UniqueKey`, `GlobalKey`).
- **BuildContext:** An object that provides information about the widget's location in the tree.
