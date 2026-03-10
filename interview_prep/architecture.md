# Software Architecture in Flutter

## Clean Architecture
Clean Architecture aims to separate concerns by dividing the software into layers. Each layer has a specific responsibility and depends only on layers "below" it.

### Layers:
1. **Domain Layer (Core):**
    - Entities (Business objects).
    - Use Cases (Application-specific business rules).
    - Repository Interfaces.
2. **Data Layer (Implementation):**
    - Data Sources (Remote/Local API clients).
    - Repository Implementations.
    - Models (to/from JSON mapping).
3. **Presentation Layer (UI):**
    - Widgets.
    - State Management (Bloc, Riverpod, etc.).

## MVVM (Model-View-ViewModel)
- **Model:** The data and business logic.
- **View:** The UI (Flutter Widgets).
- **ViewModel:** Acts as a bridge between Model and View, holding the state of the View.

## Dependency Injection (DI)
DI allows objects to receive their dependencies from an external source rather than creating them internally.

### Why use DI?
- Improves testability (easy to mock dependencies).
- Reduces coupling between classes.
- Enhances code reusability.

### Tools in Flutter:
- **Provider / Riverpod:** Often used for DI by providing dependencies down the widget tree.
- **GetIt:** A service locator for global dependency management.

---
**Next Sitting Recommendation:** [Design Patterns](./design_patterns.md) to learn reusable solutions for common architectural problems.
