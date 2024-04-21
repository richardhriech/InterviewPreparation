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



## Builder
## Prototype
## Singleton

## Also mentioning:
### Creation method / Factory method
The creation method is just a wrapper around a constructor call.