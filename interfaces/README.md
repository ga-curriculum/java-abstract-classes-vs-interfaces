# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to practice implementing interfaces by creating classes that adhere to defined contracts. 

## Demo: Interfaces (10 min)

Let's switch gears to interfaces. As we're walking through what an interface is and what it does, think about how it compares and contrasts to an abstract class.

In Java, an interface defines an API, which is essentially a contract that a class will contain the methods defined in the interface.

> **Note**: We're using API to mean "application programming interface," in that we know certain methods we can use to access something — in this case, a Java class. You may have heard the term "API" used to mean a web API, which is usually leveraged to access some sort of data. In the generic sense, an application programming interface describes that process as well.

An interface is not a class; it **cannot be instantiated**. It's just a contract declaring to the compiler that whatever instance is assigned to it will contain the methods in the interface. An interface is similar to an abstract class in that its methods are declared but not defined.

All this will become clearer when we get to the sample code. But first, let's see how to define an interface:

```java
public interface Automobile {
    // Contents
}
```

That defines the shell of an interface. The declaration of an interface is similar to a class, except it uses the `interface` keyword in place of `class`. And, like a class, an interface can have public or default (package-private) visibility.

Let's add some functionality to our `Automobile` interface:

```java
public interface Automobile {
    int getYear();
    String getMake();
    String getModel();
    void startEngine();
}
```
 
Our `Automobile` is now contracted to provide a year, make, and model, and some functionality to start the engine. Notice how these methods are defined exactly like abstract methods in abstract classes?

Now we can have some code that says something like:

```java
Automobile auto = getAutomobileById("12357"); // Get an Automobile from our database.
String make = auto.getMake();
String model = auto.getModel();
int year = auto.getYear();
auto.startEngine();
```

Note that we didn't specify any visibility for the interface methods. That's because all interface methods are always public and non-static.

-----

## Guided Practice: Implementing Interfaces (15 min)

To implement an interface means you're committing to fulfilling the interface contract for the class that implements it. 

The syntax is as follows:

```java
class MyClass implements MyInterface {
    
}
```

- `MyClass` is the class you're defining.
- `MyInterface` is the interface you're promising to enforce.

In a more concrete example, we might take our `Automobile` interface and create a `HondaAccord` class that looks like this:

```java
class HondaAccord implements Automobile {
    // Instance variable:
    private int year; 

    // Constructor:
    public HondaAccord(int year) {
        this.year = year;
    }

    // Methods that the interface needs:
    @Override
    public int getYear() {
        return this.year;
    }

    @Override
    public String getMake() {
        return "Honda";
    }

    @Override
    public String getModel() {
        return "Accord";
    }

    @Override
    public void startEngine() {
        System.out.println("Vroom vroom!");
    }
}
```

### Why Is This Important?

Let's say we're an auto manufacturing company, and last year we bought a large library of Java code from you for managing cars. We're coming out with a new kind of car, a model called Tesla Satellite, and we want to use the functionality in your `Automobile` library.

All we have to do is implement your `Automobile` interface, and we can use your existing library to manage our new car that didn't even exist when your library was written. It's one thing to write a `HondaAccord` class because we already know everything about it, but now we're able to realize the usefulness of an interface.

By **implementing** your interface, the Java compiler will ensure our new `TeslaSatellite` class has implemented all of the methods in your `Automobile` interface, thus ensuring it's usable by our libraries:

![](resources/unimplemented-interface.png)

So, let's implement those methods and try again:

![](resources/implemented-interface.png)
 
> **Tip**: As we saw before, the `@Override` annotation is optional but desirable. 

### Fields in Interfaces

Surprisingly, interfaces may contain variables, but these variables are static and **must** be assigned values in the interface. Remember that static means the field can be accessed from the interface name — as in the example below — or from any class that implements that interface. And these variables are **final**: They may not be changed, as indicated by the red underline in IntelliJ.

![](resources/reassign-interface-variable.png)

### Extending, Extending, Extending

Just like classes can extend classes, interfaces can extend other interfaces, and they inherit all the methods of the base interface. This is useful for complex systems we might encounter in real life.

Classes can also implement multiple interfaces. Let's take a look.

Think back to our `Automobile` interface. Imagine we also have a `TowVehicle` interface that deals with towing capacity, carrying capacity, and fuel type:

```java
public interface TowVehicle {
    int getCarryingCapacity();
    int getTowingCapacity();
    String getFuelType();
}
```

We might want to create a `DodgeRam` class that implements **both** interfaces. To do so, include a comma-separated list of interfaces to implement after the `implements` keyword, like this:

```java
class DodgeRam implements Automobile, TowVehicle {
    // Methods that the Automobile interface needs:
    @Override
    public int getYear() {
        return 2019;
    }

    @Override
    public String getMake() {
        return "Dodge";
    }

    @Override
    public String getModel() {
        return "Ram";
    }

    @Override
    public void startEngine() {
        System.out.println("VROOM!");
    }

    // Methods that the TowVehicle class needs:
    @Override
    int getCarryingCapacity() {
        return 2000;
    }

    @Override
    int getTowingCapacity() {
        return 13000;
    }

    @Override
    String getFuelType() {
        return "Diesel";
    }
}
```

> **Knowledge Check**: Take a second to consider the `DodgeRam` class. What methods are legal to run on it compared to the `HondaAccord` and the `TeslaSatellite` classes?

---


## Conclusion (5 min)

Both interfaces and abstract classes are used for abstraction. They're implemented in similar ways, but interfaces are most useful when you don't have any shared code between the subclasses, unlike our `Monitor` example, wherein all `Monitor` instances were able to share the `startMonitoring(String filename)` method.

Remember that interfaces:
* Cannot be instantiated.
* Cannot be static.
* Cannot implement methods.

You should use **abstract classes** when:
* You need both static and non-static methods.
* You need both abstract and non-abstract methods.
* You don't want all your fields to be `final`.

You should use **interfaces rather than abstract classes** when:
* All the methods you're defining are abstract.
* You need future developers to follow a certain pattern (this is our contract).
* You need to use more than one interface. (Remember: A class can only extend one class.)

The difference is somewhat subtle. Both interfaces and abstract classes are used for abstraction, but the key takeaway for knowing which one to use is whether or not the classes that would implement or extend the interface or abstract class will **share lines of code**.

This may require some thinking about your particular task or situation. There's no one right answer for each and every situation. It's OK, though; we trust you!