# SOLID Principles

## S: Single Responsibility Principle (SRP)
A class should have only one reason to change.
- **Example:** Separate UI logic from data fetching logic. Don't make a widget that also calls an API directly.

## O: Open-Closed Principle (OCP)
Classes should be open for extension but closed for modification.
- **Example:** Use abstract classes for repositories. If you need a new data source, create a new implementation instead of modifying the existing one.

## L: Liskov Substitution Principle (LSP)
Subclasses should be replaceable by their base classes without breaking the app.
- **Example:** If `StandardUser` and `AdminUser` both inherit from `User`, any function accepting `User` should work with both.

## I: Interface Segregation Principle (ISP)
Clients should not be forced to depend on methods they do not use.
- **Example:** Instead of one massive `Repository` interface, split it into smaller ones like `AuthRepository` and `ProductRepository`.

## D: Dependency Inversion Principle (DIP)
Depend on abstractions, not concretions. High-level modules should not depend on low-level modules.
- **Example:** A `ViewModel` should depend on an abstract `Repository` interface, not a concrete `ApiServiceImpl`.

---
**Next Sitting Recommendation:** [Dependency Injection](./di.md) to see how SOLID principles are implemented in practice.
