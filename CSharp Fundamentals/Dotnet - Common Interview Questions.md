
## OOP

### What are the OOP Principles?
- **Inheritance**: Allows a class to inherit behavior (methods) and state (fields) from another class. It promotes code reusability and is a fundamental aspect of class hierarchies.
- **Polymorphism**: Means "many shapes" and allows methods to do different things based on the object it is acting upon, which can be achieved via method overriding (same method, different classes) or method overloading (same method, different parameters).
- **Abstraction**: Abstraction focuses on what an object does instead of how it does it, providing a generic view of an object. Abstraction can be achieved with interfaces and abstract classes.
- **Encapsulation**: Involves bundling the data (attributes) and methods that operate on the data into a single unit or class. It also restricts direct access to some of an object's components, which can prevent the accidental modification of data.

### [SOLID Principles](SOLID.md)

### What are Compile-time Polymorphism and Runtime Polymorphism?

#### Compile-time Polymorphism
Compile-time polymorphism, also known as **static polymorphism**, is achieved through **method overloading** and operator overloading. It's called compile-time because the method to be executed is determined during the compilation process.
- In method overloading, a class has multiple methods with the same name but different parameters (type, number, or both).
- The compiler determines which method is intended to be called based on the method signature that best matches the arguments passed during the method call.

#### Runtime Polymorphism
Runtime polymorphism, also known as **dynamic polymorphism**, is implemented by method overriding which is a feature that allows a subclass to provide a specific implementation of a method that is already defined in its superclass. This type of polymorphism is determined at runtime.
- Method overriding occurs when a subclass has a method with the same name, return type, and parameters as a method in its parent class.
- To use method overriding, the base class method must be declared with the `virtual` keyword, and the derived class method must be declared with the `override` keyword.

## `C#`

### What are value types and reference types in C#?
- Value types hold data directly and are stored on the stack, while reference types store a reference to their data, which is held on the heap. Examples of value types include `int`, `double`, and `bool`, while `string`, arrays, and all class instances are reference types.

### What's the difference between structs and classes?
- **Memory Allocation**: Structs are value types stored on the stack, which allows for quick access but means they are better suited for small data structures. Classes are reference types stored on the heap, which is more flexible but requires overhead for memory allocation and garbage collection.
- **Inheritance**: Structs cannot inherit from another struct or class, and they cannot be the base of a class. Classes can inherit from other classes, allowing for extensive reuse of existing code.
- **Default Constructor**: Structs always have a default parameterless constructor that initializes all value types to their default value and reference fields to null. Classes can have constructors, including a parameterless one if explicitly defined.
- **Behavior on Assignment**: Assigning a struct will copy the value, so changes to one copy won’t affect another. Assigning a class instance will copy the reference, so changes to one instance reflect in all references to that object.

### What are delegates in C#?
- Delegates are type-safe function pointers that allow methods to be passed as arguments, used to define callback methods, and implement event handling.

### Explain the `static` keyword in C#.
- The `static` keyword denotes that a member belongs to the type itself rather than to any specific object. Static members are accessed by the class name rather than an instance, ensuring shared data and behavior across all instances.

### Use of `ref` and `out` Keywords
- **`ref`**: The `ref` keyword passes arguments by reference. It means any changes made to this argument in the method will be reflected in that variable when the control returns to the calling method. The referenced argument has to be initialized before being passed to the method.
- **`out`**: Similar to `ref`, but the passed argument doesn’t have to be initialized before it comes into the method. It’s also used for passing arguments by reference.

### Different Usages of the `using` Keyword
- **Using Statement**: Encapsulates the management of resources, such as file streams or database connections, ensuring that `Dispose()` is called automatically to free the resource when the block of code is done, even if an exception occurs.
- **Using Directives**: Declares a namespace to use in the file, eliminating the need for specifying the namespace each time a class or another member from this namespace is used.
- **Using Static**: Introduced in C# 6, it allows referencing static members of a class without repeating the class name.

### What is boxing and unboxing in C#?
- Boxing is the process of converting a value type to an object type, wrapping the value inside a System.Object instance on the heap. This happens implicitly. Unboxing extracts the value type from the object. This involves explicit casting. Both operations are computationally expensive.

### Describe the concept of garbage collection.
- In .NET, the garbage collector automates the management of memory by reclaiming memory occupied by objects that are no longer in use. The GC runs in the background and checks objects' accessibility. If an object is no longer referenced by any part of your code, the GC considers this object as "garbage" and frees the memory it occupies. This process helps in managing memory efficiently and avoiding memory leaks.

### How do you implement exception filtering in C#?
- Exception filtering is implemented using the `when` keyword in a catch block, allowing the catch block to handle the exception only if a specified condition is true.

### What is the Stack and What is the Heap?
- **Stack**: The stack is a region of memory that stores short-lived data such as method parameters, return addresses, and local variables. It operates in a last-in, first-out (LIFO) manner, making it very fast and suitable for data that has a known duration within a method's scope.
- **Heap**: The heap is used for dynamic memory allocation, where longer-lived data is stored, such as objects instantiated in your code. It is managed by the garbage collector, which handles allocation and deallocation of memory, helping to prevent memory leaks.

### What are the latest changes in C#?
- **C# 8.0** introduced `nullable enable`, which provides a way to explicitly declare whether a reference type is expected to handle null values or not, enhancing null safety.
- **C# 9.0** introduced `record` types for immutable data models and `init` properties to ensure properties are only settable during object initialization.
- **C# 10.0** and **C# 11.0** continued to refine these with minimal improvements, such as global using directives and improved pattern matching.

#### In more detail:
**C# 9.0 (Released with .NET 5)**
1. **Init-only Setters**: Allows properties to be made immutable more conveniently.
   ```CSharp
public class Person
{
    public string FirstName { get; init; }
    public string LastName { get; init; }
}
```
2. **Records**: Provides a way to define immutable reference types without needing to manually override equality and other methods.
```CSharp
   public record Person(string FirstName, string LastName);
```
3. **Top-level Statements**: Reduces boilerplate code for small programs, particularly useful for learning or small utility scripts.
```CSharp
System.Console.WriteLine("Hello, World!");
```
4. **Pattern Matching Enhancements**: Improvements to pattern matching, including relational patterns and logical patterns.
```CSharp
int x = 5;
if (x is > 0 and < 10)
{
    Console.WriteLine("x is between 0 and 10.");
}
```

**C# 10.0 (Released with .NET 6)**
1. **Global Using Directives**: Allows specifying a using directive that is applied globally across all files in a project.
```CSharp
global using System.Collections.Generic;
```
2. **File-scoped Namespace Declaration**: Streamlines namespace declarations to apply to the entire file, reducing nesting.
```CSharp
namespace MyApp;
```
3. **Record Structs**: Extends the record types to structs, providing value-type records.
```CSharp
public record struct Point(int X, int Y);
```

**C# 11.0 (Released with .NET 7)**
1. **List Patterns**: Allows matching sequences in a collection more succinctly in pattern matching.
```CSharp
var numbers = new[] { 1, 2, 3 };
if (numbers is [1, 2, 3])
{
    Console.WriteLine("Matched the sequence 1, 2, 3!");
}
```
2. **Required Properties**: Ensures that properties must be initialized when an object is created.
```CSharp
public class Person
{
    public string FirstName { get; required }
    public string LastName { get; required }
}
```
3. **Raw String Literals**: Allows for multiline strings and ignores escaped sequences making it easier to work with JSON, XML, or regular expressions directly in the code.
```CSharp
string json = """
{
    "name": "John",
    "age": 30
}
""";
```

### What is the Relationship Between .NET Versions and C# Language Versions?
Sure, let’s discuss the latest changes introduced in recent C# versions and explain the relationship between .NET versions and C# language versions.

### Latest Changes in C# Versions
**C# 9.0 (Released with .NET 5)**
1. **Init-only Setters**: Allows properties to be made immutable more conveniently.
   ```csharp
   public class Person
   {
       public string FirstName { get; init; }
       public string LastName { get; init; }
   }
   ```
2. **Records**: Provides a way to define immutable reference types without needing to manually override equality and other methods.
   ```csharp
   public record Person(string FirstName, string LastName);
   ```

3. **Top-level Statements**: Reduces boilerplate code for small programs, particularly useful for learning or small utility scripts.
   ```csharp
   System.Console.WriteLine("Hello, World!");
   ```

4. **Pattern Matching Enhancements**: Improvements to pattern matching, including relational patterns and logical patterns.
   ```csharp
   int x = 5;
   if (x is > 0 and < 10)
   {
       Console.WriteLine("x is between 0 and 10.");
   }
   ```

**C# 10.0 (Released with .NET 6)**
1. **Global Using Directives**: Allows specifying a using directive that is applied globally across all files in a project.
   ```csharp
   global using System.Collections.Generic;
   ```
2. **File-scoped Namespace Declaration**: Streamlines namespace declarations to apply to the entire file, reducing nesting.
   ```csharp
   namespace MyApp;
   ```
3. **Record Structs**: Extends the record types to structs, providing value-type records.
   ```csharp
   public record struct Point(int X, int Y);
   ```

**C# 11.0 (Released with .NET 7)**
1. **List Patterns**: Allows matching sequences in a collection more succinctly in pattern matching.
   ```csharp
   var numbers = new[] { 1, 2, 3 };
   if (numbers is [1, 2, 3])
   {
       Console.WriteLine("Matched the sequence 1, 2, 3!");
   }
   ```
2. **Required Properties**: Ensures that properties must be initialized when an object is created.
   ```csharp
   public class Person
   {
       public string FirstName { get; required }
       public string LastName { get; required }
   }
   ```
3. **Raw String Literals**: Allows for multiline strings and ignores escaped sequences making it easier to work with JSON, XML, or regular expressions directly in the code.
   ```csharp
   string json = """
   {
       "name": "John",
       "age": 30
   }
   """;
   ```

### Relationship Between .NET Versions and C# Language Versions
C# language versions are tied to .NET implementations. Each major release of .NET typically comes with a new version of C#. Here’s how it generally works:

- **.NET Framework** was traditionally bundled with new versions of Visual Studio and included updates to the C# language. For example, .NET Framework 4.6 came with C# 6.0.
- **.NET Core** introduced a faster release cycle, with each major version bringing new language features. For instance, .NET Core 3.1 supported C# 8.0.
- **.NET 5 and onwards** (the unification of .NET Core and .NET Framework into a single platform called .NET) continues this trend. For example, .NET 5 supports C# 9.0, .NET 6 supports C# 10.0, and .NET 7 supports C# 11.0.

Developers can generally use the latest C# features by targeting the latest version of .NET but may need to set the language version explicitly in the project file if they need specific features while targeting older .NET versions.

This alignment ensures that the .NET platform and the C# language evolve together, providing a cohesive development experience.

### [DI Life Cycles](../DependencyInjection/DI%20Life%20Cycles.md)

### [Threads - Interview Questions](Threads/Threads%20-%20Interview%20Questions.md)