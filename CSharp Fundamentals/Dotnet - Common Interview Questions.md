### What are value types and reference types in C#?
- **Answer**: Value types hold data directly and are stored on the stack, while reference types store a reference to their data, which is held on the heap. Examples of value types include `int`, `double`, and `bool`, while `string`, arrays, and all class instances are reference types.
### How does the `using` statement benefit resource management in C#?
- **Answer**: The `using` statement ensures that the object implementing the `IDisposable` interface disposes of its resources automatically when the control leaves the block, helping manage resources efficiently, such as file handles and database connections.
### Explain the difference between `struct` and `class` in C#.
- **Answer**: Structs are value types and are stored on the stack, leading to faster access but limited functionality. Classes are reference types, stored on the heap, and allow for inheritance and data encapsulation, suitable for larger data structures.
### Explain polymorphism in C#.
- *Answer**: Polymorphism allows methods to have the same name but behave differently based on the object that invokes them. This can be achieved either through ***method overriding (runtime polymorphism)*** or ***method overloading (compile-time polymorphism)***.
### What are delegates in C#?
- **Answer**: Delegates are type-safe function pointers that allow methods to be passed as arguments, used to define callback methods, and implement event handling.
### Explain the `static` keyword in C#.
- **Answer**: The `static` keyword denotes that a member belongs to the type itself rather than to any specific object. Static members are accessed by the class name rather than an instance, ensuring shared data and behavior across all instances.
### What is boxing and unboxing in C#?
- **Answer**: Boxing is the process of converting a value type to an object type, wrapping the value inside a System.Object instance on the heap. Unboxing extracts the value type from the object. Both operations are computationally expensive.
### Describe the concept of garbage collection in C#.
- **Answer**: Garbage collection is the process of automatically reclaiming memory by removing objects that are no longer in use. C# manages memory through a garbage collector that runs periodically to free unused objects.
### How do you implement exception filtering in C#?

- **Answer**: Exception filtering is implemented using the `when` keyword in a catch block, allowing the catch block to handle the exception only if a specified condition is true.