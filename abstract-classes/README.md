<h1>
  <span class="headline">Java Abstract Classes vs. Interfaces</span>
  <span class="subhead">Abstract Classes</span>
</h1>

**Learning objective:** By the end of this lesson, you'll be able code flexible, reusable, and scalable java programs using abstract classes.

## An introduction to abstract classes
In Object Oriented Programming, abstraction is the technique of reducing complexity by:
- Hiding unnecessary information.
- Exposing only necessary information.

There are two types of explicity abstract entities in Java:
### 1. Abstract Methods
 - Contain a method signature (method name and arguments).
 - Do not contain a method body (statement block `{}`).
 - Do not exist to be functional.
 - Exist only for enforcing subclasses to implement the method body.
 - Are differentiated from concrete methods using `abstract` keyword in their declaration. 
   - For example: 
      ```java
      public abstract double calculateArea();
      ```
      Note that the method signatures have no braces `{}` and are terminated with a semicolon.
 ### 2. Abstract Classes
 - Must contain atleast one abstract method.
 - Can contain instance variables, constructors, static methods and other concrete methods.
 - Cannot be instantiated into objects
 - Exist only to be extended by subclasses which then need to implement the abstract methods.
 - Are differentiated from concrete methods using `abstract` in their declaration.

## Defining an abstract class
```java
// Abstract class representing the blueprint for all animals
abstract class Animal {
    String name;

    // Constructor
    public Animal(String name) {
        this.name = name;
    }

    // Concrete method (shared behavior)
    public void eat() {
        System.out.println(name + " is eating.");
    }

    // Abstract method (unique behavior)
    public abstract void move();
}
```
## Extending an abstract class
```java
class Bird extends Animal {
    public Bird(String name) {
        super(name);
    }

    // Implementing the abstract method
    @Override
    public void move() {
        System.out.println(name + " is flying.");
    }
}

class Fish extends Animal {
    public Fish(String name) {
        super(name);
    }

    // Implementing the abstract method
    @Override
    public void move() {
        System.out.println(name + " is swimming.");
    }
}

class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }

    // Implementing the abstract method
    @Override
    public void move() {
        System.out.println(name + " is running.");
    }
}
```
**Note**: `super()` is used to call the constructor of the superclass from the subclass constructor, which is essential for initializing inherited members.

## Instantiating a subclass under contract
```java
public class AnimalDemo {
    public static void main(String[] args) {
        // Create instances of subclasses
        Animal bird = new Bird("Parrot");
        Animal fish = new Fish("Goldfish");
        Animal dog = new Dog("Bulldog");

        // Call methods
        bird.eat();
        bird.move();

        fish.eat();
        fish.move();

        dog.eat();
        dog.move();
    }
}
```
<Details>
<summary>Expected Output</summary>
<code>

Parrot is eating.

Parrot is flying.

Goldfish is eating.

Goldfish is swimming.

Bulldog is eating.

Bulldog is running.

</code>
</Details>


## Independent practice

(5 mins)

1. Find out what happens when you try to extend an abstract class but do not implement one of its abstract methods in your code. You can use the example code from _Extending an abstract class_ topic.
2. Find out what happens when you try to instantiate an abstract class in your code. You can use the example from _Instantiating a subclass under contract_ topic.
