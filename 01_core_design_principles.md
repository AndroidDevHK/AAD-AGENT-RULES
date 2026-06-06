# Rule 1: Core Design Principles

When generating or refactoring code for Android App Development, you MUST strictly adhere to the following core design principles. These are non-negotiable foundations for all generated code.

## 1. Separation of Concerns (SoC)
Ensure that the code is divided into distinct sections, where each section addresses a separate concern.
- **UI Logic**: Keep UI components (Activities, Fragments, Composables) strictly focused on rendering data and handling user interactions.
- **Business Logic**: Isolate business rules and domain logic in UseCases, Interactors, or ViewModels.
- **Data Access**: Delegate all data fetching and storage (network, database, preferences) to distinct Repository classes.

## 2. Object-Oriented Programming (OOP)
Apply fundamental OOP concepts correctly to ensure the code is modular, reusable, and easy to maintain.
- **Encapsulation**: Keep class fields private and expose only necessary functionality through public methods or properties.
- **Abstraction**: Hide complex implementation details behind simple interfaces.
- **Inheritance & Polymorphism**: Use inheritance where a clear "is-a" relationship exists, but prefer composition over inheritance to prevent rigid class hierarchies.

## 3. SOLID Principles
Every class and module must be designed with SOLID principles in mind:
- **S - Single Responsibility Principle (SRP)**: A class should have only one reason to change.
- **O - Open/Closed Principle (OCP)**: Software entities should be open for extension but closed for modification.
- **L - Liskov Substitution Principle (LSP)**: Subtypes must be substitutable for their base types without altering the correctness of the program.
- **I - Interface Segregation Principle (ISP)**: Do not force clients to implement interfaces they do not use. Prefer smaller, more specific interfaces.
- **D - Dependency Inversion Principle (DIP)**: High-level modules should not depend on low-level modules; both should depend on abstractions. Use Dependency Injection (e.g., Hilt, Dagger).

## 4. Zero Redundancy (DRY - Don't Repeat Yourself)
Eliminate code duplication entirely.
- **Reusable Components**: If you find yourself writing the same logic or UI component more than once, extract it into a separate, reusable function, class, or Composable.
- **Constants & Resources**: Hardcoded strings, dimensions, and colors must be extracted to the appropriate resource files (`strings.xml`, `colors.xml`) or defined as constants.
- **Utility Functions**: Group common operations into shared utility or extension functions.

## 🌟 Benefits of Adhering to these Rules
By strictly following these core design principles, the generated code will have the following benefits:
- **Maintainability**: Code is easy to understand, modify, and fix without causing unintended side-effects.
- **Testability**: Separated concerns and dependency injection make it trivial to write automated unit and integration tests.
- **Scalability**: New features can be added with minimal changes to existing, working code (Open/Closed Principle).
- **Reduced Bugs**: Avoiding redundancy and having single responsibilities means fewer places for bugs to hide and easier debugging.
- **Team Collaboration**: Standardized architecture makes it easier for human developers to read and collaborate on the AI-generated code.
