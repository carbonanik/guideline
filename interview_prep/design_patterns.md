# Design Patterns

Design patterns are reusable solutions to common problems in software design.

## 1. Creational Patterns (Object Creation)

### Singleton
Ensures a class has only one instance and provides a global point of access.
- **Example:** A database helper or a global configuration object.
- **Dart Tip:** Use a private constructor and a static instance.

### Factory
Defines an interface for creating objects but lets subclasses decide which class to instantiate.
- **Example:** Different types of `Button` widgets (Material vs. Cupertino).

## 2. Structural Patterns (Object Relationships)

### Adapter
Allows incompatible interfaces to work together.
- **Example:** Wrapping a 3rd party library to match your internal architecture.

### Decorator
Dynamically adds behavior to an object without affecting others.
- **Flutter Example:** Wrapping a `Widget` with a `Padding` or `Center` widget.

## 3. Behavioral Patterns (Object Communication)

### Observer
Notifies multiple objects about any state changes in the observed object.
- **Flutter Example:** `ChangeNotifier`, `ValueListenableBuilder`.

### Strategy
Defines a family of algorithms and makes them interchangeable.
- **Example:** Different payment methods (Credit Card, PayPal) that share the same checkout interface.

### Command
Turns a request into a stand-alone object containing all information about the request.
- **Example:** Undo/Redo operations.

---
**Next Sitting Recommendation:** [SOLID Principles](./solid.md) to understand the fundamentals of clean object-oriented design.
