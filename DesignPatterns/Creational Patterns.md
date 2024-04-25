Creational patterns are focused towards how to ***instantiate*** an object or group of related objects.

[Comparison of different factories](https://refactoring.guru/design-patterns/factory-comparison)

- [Simple Factory](#Simple%20Factory)
- [Factory Method](#Factory%20Method)
- [Abstract Factory](#Abstract%20Factory)
- [Builder](#Builder)
- [Prototype](#Prototype)
- [Singleton](#Singleton)
- [Also mentioning](#Also%20mentioning)

## Simple Factory

Simple factory simply ***generates an instance*** for client ***without exposing*** any instantiation ***logic*** to the client.

The Simple Factory pattern describes ***a class that has one creation method*** with a large conditional that based on method parameters chooses which product class to instantiate and then return.

### When to use?
The Simple Factory pattern is useful when creating objects that share a common interface but differ in some details, and you want to abstract the logic that decides which specific class to instantiate.

### Example
```CSharp
public static IUser Create(string type)
    {
        switch (type.ToLower())
        {
            case "user":
                return new User();
            case "customer":
                return new Customer();
            case "admin":
                return new Admin();
            default:
                throw new ArgumentException("Wrong user type passed.");
        }
    }
```
## Factory Method
The Factory Method is a creational design pattern that ***provides an interface for creating*** objects but allows subclasses to alter the type of an object that will be created.

In other words:
It provides a way to delegate the instantiation logic to child classes.

### Example
```CSharp
public abstract class Department
{
    public abstract IEmployee CreateEmployee(int id);

    public void Fire(int id)
    {
        IEmployee employee = CreateEmployee(id);
        employee.PaySalary();
        employee.Dismiss();
    }
}

public class ITDepartment : Department
{
    public override IEmployee CreateEmployee(int id)
    {
        return new Programmer(id);
    }
}

public class AccountingDepartment : Department
{
    public override IEmployee CreateEmployee(int id)
    {
        return new Accountant(id);
    }
}

```

### When to use?
Useful when there is some generic processing in a class but the required sub-class is dynamically decided at runtime. Or putting it in other words, when the client doesn’t know what exact sub-class it might need.

## Abstract Factory
A factory of factories; a factory that groups the individual but related/dependent factories together without specifying their concrete classes.

### Example

#### Interfaces

```Csharp
// Interface for Door
public interface IDoor
{
    void GetDescription();
}

// Interface for DoorFittingExpert
public interface IDoorFittingExpert
{
    void GetDescription();
}

// Interface for DoorFactory
public interface IDoorFactory
{
    IDoor MakeDoor();
    IDoorFittingExpert MakeFittingExpert();
}
```

#### Concrete classes

```CSharp
// WoodenDoor implements IDoor
public class WoodenDoor : IDoor
{
    public void GetDescription()
    {
        Console.WriteLine("I am a wooden door");
    }
}

// IronDoor implements IDoor
public class IronDoor : IDoor
{
    public void GetDescription()
    {
        Console.WriteLine("I am an iron door");
    }
}

// Welder implements IDoorFittingExpert
public class Welder : IDoorFittingExpert
{
    public void GetDescription()
    {
        Console.WriteLine("I can only fit iron doors");
    }
}

// Carpenter implements IDoorFittingExpert
public class Carpenter : IDoorFittingExpert
{
    public void GetDescription()
    {
        Console.WriteLine("I can only fit wooden doors");
    }
}

// WoodenDoorFactory implements IDoorFactory
public class WoodenDoorFactory : IDoorFactory
{
    public IDoor MakeDoor()
    {
        return new WoodenDoor();
    }

    public IDoorFittingExpert MakeFittingExpert()
    {
        return new Carpenter();
    }
}

// IronDoorFactory implements IDoorFactory
public class IronDoorFactory : IDoorFactory
{
    public IDoor MakeDoor()
    {
        return new IronDoor();
    }

    public IDoorFittingExpert MakeFittingExpert()
    {
        return new Welder();
    }
}
```

#### Usage
```CSharp
// Using the Wooden Door Factory
IDoorFactory woodenFactory = new WoodenDoorFactory();
IDoor door = woodenFactory.MakeDoor();
IDoorFittingExpert expert = woodenFactory.MakeFittingExpert();

door.GetDescription();  // Output: I am a wooden door
expert.GetDescription(); // Output: I can only fit wooden doors

// Using the Iron Door Factory
IDoorFactory ironFactory = new IronDoorFactory();
door = ironFactory.MakeDoor();
expert = ironFactory.MakeFittingExpert();

door.GetDescription();  // Output: I am an iron door
expert.GetDescription(); // Output: I can only fit iron doors
```

## Builder
https://refactoring.guru/design-patterns/builder
Builder lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

### The problem
In some cases you might want to avoid creating a subclass for variations of the same class, but that can result in complicated, long constructors.
![](../Media/Pasted%20image%2020240421180716.png)
 ![](../Media/Pasted%20image%2020240421184959.png)

### The Solution
The Builder pattern lets you construct complex objects ***step by step***. The Builder doesn’t allow other objects to access the product while it’s being built.

Some of the steps might need different implementations when you need various versions of the product. In this case you can create several different builder classes, implementing the same set of steps.

You can extract the series of step calls into a separate ***Director*** class that defines the order in which to call the steps.

![](../Media/Pasted%20image%2020240421185836.png)

### When to use?
When there could be several flavors of an object and to avoid the constructor telescoping. The key difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.

## Prototype
Create an object based on an existing object through cloning.

### Problem 
You might want to create an exact copy of an instance. In regular copying some of the objects' properties may be private, so the copied object might behave differently.

### Solution
The class should implement a ***Prototype*** interface, containing a ***Clone*** method (or a constructor that accepts a parameter from the same class). This method now has access to private fields and other implementation details "from the inside", so it can create a required copy of the original instance.

Implementation details: https://refactoring.guru/design-patterns/prototype

### Cons
Cloning complex objects that have circular references might be very tricky.

## Singleton
https://refactoring.guru/design-patterns/singleton
The pattern ensures that only one instance of a particular class is ever created.

Could be useful when you want to control access to a shared resource.
### Requirements
1. Ensure that the class can have only one instance.
1. Provide a global access point to the instance from anywhere in the program. It also protects it from being overwritten.

### Cons
- creates a global state of your app: a change in one place can affect another part of the application
	- bugs introduced by this are hard to find
- makes your code tightly coupled
- mocking can be difficult

### Structure
![](../Media/Pasted%20image%2020240421194516.png)
```CSharp
public sealed class President
{
    private static readonly President instance = new President();
    private static readonly object padlock = new object();
    
    // Private constructor ensures that an object is not instantiated from outside the class
    private President()
    {
    }

    public static President Instance
    {
        get
        {
            lock (padlock)
            {
                return instance;
            }
        }
    }
}
```

1. **Sealed Class**: The `sealed` keyword prevents the class from being inherited.
2. **Static Initialization**: The Singleton instance is created using a static initializer. This ensures thread safety and lazy initialization by default due to .NET's handling of static constructors.
3. **Thread Safety**: The use of a lock (`padlock`) ensures that the instance is thread-safe and handles multi-threaded scenarios safely. However, in this particular case since the instance is already initialized statically, the lock is not necessarily required for instance creation but might be useful if later modification or operations need to be thread-safe.
4. **No Need for Clone or Deserialize Prevention**: Unlike PHP, in C#, if you do not provide cloning (ICloneable interface) or serialization capabilities, the class won't be cloneable or serializable.
## Also mentioning

### Creation method / Factory method
The creation method is just a wrapper around a constructor call.