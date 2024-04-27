### What are the SOLID Principles?
- **Single Responsibility Principle (SRP)**: Each class should have one and only one reason to change, meaning it should have only one job or responsibility.
- **Open/Closed Principle (OCP)**: Software entities should be open for extension, but closed for modification. This means you can add new features via extensions without changing existing code.
- **Liskov Substitution Principle (LSP)**: Objects of a superclass shall be replaceable with objects of its subclasses without affecting the functionality of the program. This defines rules for a good inheritance structure.
- **Interface Segregation Principle (ISP)**: Larger interfaces should be split into smaller ones. By doing so, a class will only have to know about the methods that are of interest to them.
- **Dependency Inversion Principle (DIP)**: 
1. High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces or abstract classes).
2. Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.