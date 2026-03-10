# Testing Strategies

Seniors aren't just expected to write code; they are expected to ensure its quality through testing.

## 1. The Testing Pyramid

### Unit Testing
Tests a single function, method, or class.
- **Goal:** Verify business logic (e.g., a BLoC/Notifier, a Repository, or a Utility function).
- **Tool:** `test` package.
- **Mocking:** Use `mockito` or `mocktail`.

### Widget Testing
Tests a single widget.
- **Goal:** Verify that the UI looks and behaves as expected (e.g., tapping a button triggers a callback).
- **Tool:** `flutter_test` (part of Flutter SDK).
- **Key Method:** `tester.pumpWidget()`, `tester.tap()`, `tester.pumpAndSettle()`.

### Integration Testing
Tests the whole app or a large part of it.
- **Goal:** Verify that all layers work together correctly (e.g., login flow from UI to API).
- **Tool:** `integration_test` package.

## 2. Key Concepts

### Pumping
- `pump()`: Triggers a rebuild (one frame).
- `pumpAndSettle()`: Repeatedly calls `pump()` until there are no more scheduled frames (waits for animations to finish).

### Finders
Used to locate widgets in the tree: `find.byType()`, `find.byKey()`, `find.text()`.

### Mocking vs. Faking
- **Mock:** An object where you record and verify expectations (e.g., "was this method called twice?").
- **Fake:** A working implementation with a simplified version of the logic (e.g., an in-memory database).

## 3. What to Test?
- **Business Logic:** 100% coverage if possible.
- **Complex UI:** Test edge cases and interactions.
- **Avoid:** Testing static UI (like a `Text` widget that never changes).

---
**Next Sitting Recommendation:** [Native Communication](./native_communication.md) to handle platform-specific features.
