Creational patterns are focused towards how to ***instantiate*** an object or group of related objects.

[Comparison of different factories](https://refactoring.guru/design-patterns/factory-comparison)

- [[#Simple Factory|Simple Factory]]
- [[#Factory Method|Factory Method]]
- [[#Abstract Factory|Abstract Factory]]
- [[#Builder|Builder]]
- [[#Prototype|Prototype]]
- [[#Singleton|Singleton]]
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
![[Pasted image 20240421180716.png]]
### The Solution

![[Pasted image 20240421184959.png]]
The Builder pattern lets you construct complex objects ***step by step***. The Builder doesn’t allow other objects to access the product while it’s being built.

Some of the steps might need different implementations when you need various versions of the product. In this case you can create several different builder classes, implementing the same set of steps.

You can extract the series of step calls into a separate ***Director*** class that defines the order in which to call the steps.

![[Pasted image 20240421185836.png]]
### When to use?

When there could be several flavors of an object and to avoid the constructor telescoping. The key difference from the factory pattern is that; factory pattern is to be used when the creation is a one step process while builder pattern is to be used when the creation is a multi step process.

## Prototype
Create an object based on an existing object through cloning.

### Problem 
You might want to create an exact copy of an instance. In regular copying some of the objects' properties may be private, so the copied object might behave differently.

### Solution
The class should implement a ***Prototype*** interface, containing a ***Clone*** method (or a constructor that accepts a parameter from the same class). This method now has access to private fields and other implementation details "from the inside", so it can create a required copy of the original instance.

Implementation details: https://refactoring.guru/design-patterns/prototype

## Singleton

## Also mentioning:
### Creation method / Factory method
The creation method is just a wrapper around a constructor call.