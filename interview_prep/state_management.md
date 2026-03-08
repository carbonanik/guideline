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
- **Cubit:** A simpler version of Bloc that uses methods instead of events.

## Riverpod vs. BLoC vs. Provider

| Feature | Provider | Riverpod | BLoC |
| --- | --- | --- | --- |
| **Complexity** | Low | Medium | High |
| **Boilerplate** | Medium | Low | High |
| **Testability** | Good | Excellent | Excellent |
| **Safety** | Runtime (can fail) | Compile-time | Excellent |
| **Context** | Required | Optional (via Ref) | Required |

### Question: "When to choose BLoC over Riverpod?"
**Answer:** Choose **BLoC** if you want strict event-driven architecture and the strongest possible separation of UI and logic. Choose **Riverpod** if you want faster development speed, less boilerplate, and a more modern Dart feel.

---
**Next Sitting Recommendation:** [Riverpod Deep Dive](https://github.com/carbonanik/guideline/blob/master/interview_prep/riverpod.md)
