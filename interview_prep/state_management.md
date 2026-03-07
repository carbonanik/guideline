# State Management

## Why do we need it?
Flutter is a declarative framework. The UI is a function of the state (`UI = f(state)`). State management helps us:
- Share data across different screens.
- Manage side effects (API calls, data persistence).
- Keep code organized and testable.

## Ephemeral vs. App State
- **Ephemeral State:** Local to a single widget (e.g., current page in a PageView, text in a controller). Use `setState`.
- **App State:** Shared across the entire app (e.g., login status, user preferences, shopping cart). Use a state management library.

## Comparison of Common Tools

### Provider
- Built on `InheritedWidget`.
- Simple and easy to learn.
- Recommended by the Flutter team for many use cases.

### BLoC (Business Logic Component)
- Uses **Streams** for event-driven state management.
- Clearly separates events (inputs) from states (outputs).
- Great for large, complex apps with rigorous testing requirements.

### GetX
- Provides state management, dependency injection, and routing in one.
- High performance and low boilerplate.
- Can be controversial due to its deviation from standard Flutter patterns.

### Riverpod
- A rewrite of Provider by the same author.
- Solves many Provider limitations (no global dependencies, compile-time safety).
