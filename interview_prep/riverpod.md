# Riverpod

Riverpod is a powerful, compile-time safe state management library for Flutter.

## Why Riverpod over Provider?
1. **Compile-time Safety:** No more `ProviderNotFoundException`.
2. **No BuildContext Required:** Providers can be accessed from anywhere (with a `Ref`).
3. **Multiple Providers of the same type:** You can define as many as you need without conflict.

## Core Concepts

### 1. `ProviderScope`
Must wrap the entire application to store the state of all providers.

### 2. Provider Types
- **`Provider`:** Great for simple values and dependency injection.
- **`FutureProvider`:** Handles asynchronous data fetching (e.g., API calls).
- **`StreamProvider`:** Similar to `FutureProvider` but for data that changes over time (e.g., Firebase Auth status).
- **`StateNotifierProvider` / `NotifierProvider`:** Best for complex states that can be modified via methods.

### 3. Consuming Providers
- **`ConsumerWidget`:** A stateless widget that has access to `WidgetRef`.
- **`ConsumerStatefulWidget`:** A stateful widget that has access to `ref`.
- **`Consumer` Widget:** For localized rebuilds inside a `build` method.

## Useful Methods
- `ref.watch(provider)`: Listens to the provider and rebuilds the widget when the state changes.
- `ref.read(provider)`: Reads the current state once (usually in callbacks).
- `ref.listen(provider, (previous, next) { ... })`: Performs side effects without rebuilding.
- `ref.invalidate(provider)`: Forces a provider to refresh its state.
