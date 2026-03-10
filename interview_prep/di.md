# Dependency Injection (DI)

Dependency Injection is not just a pattern; it's a way to ensure your app is modular and testable.

## 1. Why explicit DI?
- **Decoupling:** High-level modules don't depend on low-level implementation.
- **Mocking:** Easy to swap a real API service with a mock one during tests.
- **Single Source of Truth:** One place to configure your app's dependencies.

## 2. Common Tools

### GetIt
A simple Service Locator for Dart and Flutter. It’s NOT a widget, so it’s fast and doesn't need `BuildContext`.
```dart
final getIt = GetIt.instance;
getIt.registerSingleton<AuthService>(AuthServiceImpl());
```

### Injectable
A code generator for `GetIt`. It removes the manual registration boilerplate.
- Use `@module`, `@singleton`, and `@injectable` annotations.

### Riverpod as DI
Riverpod is unique because it handles BOTH state management and dependency injection.
```dart
final authServiceProvider = Provider<AuthService>((ref) => AuthServiceImpl());
```

## 3. Dependency Inversion (The 'D' in SOLID)
Don't depend on `ApiServiceImpl`. Depend on `ApiService` (the interface).

### Interview Question: "Service Locator vs. Dependency Injection?"
**Answer:** In pure **Dependency Injection**, objects are *given* their dependencies (e.g., via constructor). In a **Service Locator** (like GetIt), objects *request* their dependencies. Senior developers usually prefer constructor injection for visibility and easier unit testing.

---
**Next Sitting Recommendation:** [Testing](./testing.md) to see DI in action.
