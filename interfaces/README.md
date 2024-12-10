<h1>
  <span class="headline">Java Abstract Classes vs. Interfaces</span>
  <span class="subhead">Interfaces</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be able to:
- Code flexible, reusable, and scalable java programs using interfaces.
- Decide when to use interfaces and when to use abstract classes.

## An introduction to interfaces
An abstract class is mandated to have only one abstract method. In an abstract class, only abstract methods can enforce a contractual relationship with any subclass that extends the abstract class. Additionally, it is allowed to have other concrete methods which have no obligation to enforce a contract, like a traditional class implementation. Hence abstract classes are termed as **partial implementations** as opposed to a contract. They are still classes. 

An **interface**, on the other hand, are not classes. They are purely contracts. The sole purpose of their existence is to act as a contract for class that implement them. Consequentially, interfaces differ from abstract classes (and classes in general) in many ways. Lets explore these differences.

## Differences between abstract classes and interfaces

### 1. Declaration 
Interfaces use `interface` keyword whereas abstract classes use `abstract` and `class` keywords.

Interface declaration:
```java
public interface Animal {
    // Interface members
}
```
Abstract class declaration:
```java
public abstract class Animal {
    //Abstract class members
}
```

### 2. Abstract methods as members
While abstract classes can contain both abstract methods (without implementation) and concrete methods (with implementation), In interfaces, all methods are implicitly abstract. They need not have `abstract` keyword. It is illegal to provide method implementations for interface methods. 

```java
// Interface with abstract method
public interface Animal {
    void makeSound();  // Abstract method, no implementation
    
    }
}

// Abstract class with abstract and concrete methods
public abstract class Animal {
    public void sleep() {
        System.out.println("Animal is sleeping");  // Concrete method
    }
    
    public abstract void makeSound();  // Abstract method
}
```

### 3. Inheritance style
Since abstract classes are still considered classes, subclasses use `extends` keyword to inherit from an abstract class. And also, the single inhertence rule of classes is still applicable to abstract classes. In other words, a subclass can **extend** only one abstract class as their superclass.

Classes inheriting from interfaces use `implements` keyword. A class is allowed **implement** more than one interface.

Implementing interfaces:
```java
// Interface 1
public interface Animal {
    void makeSound();
}

// Interface 2
public interface Movable {
    void move();
}

// Class implementing multiple interfaces
public class Dog implements Animal, Movable {
    public void makeSound() {
        System.out.println("Woof!");
    }
    
    public void move() {
        System.out.println("The dog is moving");
    }
}
```

Extending abstract classes:
```java
// Abstract class 1
public abstract class Animal {
    public abstract void makeSound();
}

// Abstract class 2 (not allowed)
public abstract class Movable {
    public abstract void move();
}

// Class extending one abstract class
public class Dog extends Animal {
    public void makeSound() {
        System.out.println("Woof!");
    }
}
```

### 4. Constructors
Interfaces cannot have constructors because they cannot be instantiated directly. The purpose of an interface is to provide a contract, not to create objects.

Abstract classes, however, can have constructors. These constructors can be used by subclasses to initialize the state of the abstract class.
```java
// Interface: No constructors allowed
public interface Animal {
    void makeSound();
}

// Abstract class: Has a constructor
public abstract class Animal {
    private String name;
    
    public Animal(String name) {
        this.name = name;
    }
    
    public abstract void makeSound();
}
```

### 5. Access modifiers for methods
In interfaces, methods are implicitly public, meaning they are accessible from anywhere and dont need the `public` keyword. We cannot specify a more restrictive access modifier like `private` or `protected`.

Abstract classes allow methods to have any access modifier (`public`, `protected`, or `private`)
```java
// Interface: Methods are public by default
public interface Animal {
    void makeSound();  // Implicitly public
}

// Abstract class: Can have any access modifier
public abstract class Animal {
    public abstract void makeSound();  // Public method
    
    protected abstract void move();   // Protected method
    
    private abstract void eat();      // Private method
}
```
### 6. Variables
Interfaces can only have only variables that are implicitly `static` + `final`. In other words, interfaces can have only constants. They cannot have instance variables.

Abstract classes can have both instance variables and static variables.
```java
// Interface: Can only have static final variables
public interface Animal {
    String SPECIES = "Canine";  // Implicitly static final
}

// Abstract class: Can have instance variables
public abstract class Animal {
    private String name;  // Instance variable
    
    public abstract void makeSound();
}
```

## Key Takeaway
- Interfaces are best suited for defining a contract that can be followed by multiple classes. They allow for multiple inheritance, but cannot provide any implementation.
- Abstract classes are best suited for providing a base class with some shared behavior that can be extended by subclasses. They allow for a mixture of abstract and concrete methods and can have instance variables and constructors.