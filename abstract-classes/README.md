# ![[tktk Module Name] - tktk Microlesson Name](./assets/hero.png)

**Learning objective:** By the end of this lesson, students will be able to implement abstract classes in Java using the template method design pattern.

## Opening (5 min)

There are times when you want to implement some behavior in a class but want another developer to implement some other behavior.

For instance, in our earlier example of the `Shape` class, we provided a default implementation for the `getCircumference()` and `getArea()` methods:

```java
public class Shape {
    public double getCircumference() {
        return 0;
    }

    public double getArea() {
        return 0;
    }
}

```

In that example, both returned `0`.

Now suppose a different developer implemented a subclass, such as `Circle`, and they weren't clear that the initial developer of the `Shape` class intended those two methods to be overridden to provide an implementation. Then, they would leave those unimplemented and we would suddenly find circles with circumferences and areas equal to zero.

----

## Demo: Abstract Classes (10 min)

To prevent this sort of communication breakdown, the developer of the `Shape` class can mark it as an **abstract class**. Abstract classes allow us to define abstract methods that **force** the developer to define an implementation. If they don't, the Java compiler will throw an error.

An abstract method can **only** be defined in an abstract class. To define an abstract class, put `abstract` before the `class` keyword:

```java
public abstract class Shape {
    // Contents
}
``` 

With that done, we can now define some abstract methods. These get a method signature and return type but don't get an implementation. The return type must be preceded by the `abstract` keyword, as in the following example:

```java

public abstract class Shape {
        public abstract double getCircumference();

        public abstract double getArea();
}

```

By seeing this, the developer and Java compiler both understand that there must be an implementation of a method called `getCircumference()` in a subclass of `Shape` and that it must return a `double` result. 

**What if we forget to implement a method marked as `abstract`?**

Let's say we wanted to create a `Circle` subclass, but we forgot to implement the `getArea()` method.

![](resources/failed-to-implement-abstract.png)

You can see that IntelliJ warns us — with a big red underline and a fat dialog box — that our class is doomed to fail when compiling.

Once we implement the missing method, everything will go back to normal:

![](resources/implement-abstract.png)

----

## Guided Practice: Abstract Classes in Action (10 min) 

A common use of abstract classes is to implement a **framework** or **template method** design pattern. This pattern allows the framework to define the larger behavior, leaving the particulars to the framework developer.

Suppose we want to create a framework that does some (undefined) processing and writes the results to a file. This is a common operation in monitoring applications, where input could come from a database, files, event logs, devices, and more. It's a perfect use case for abstract classes.

> **Note**: We purposely design the abstract class as generic so subclasses can handle potentially any of these cases.

We want to process that information by writing individual `Monitor` subclasses that call the `process()` method and write the result to the file system.

Let's write a base abstract class called `AbstractMonitor`, with an abstract method called `process()` that returns a `String`, and a non-abstract method called `startMonitoring(String fileName)`:

```java
public abstract class AbstractMonitor {
    public abstract String process();
    
    public void startMonitoring(String fileName) throws IOException, InterruptedException {
        while(true) {
            String value = process();

            RandomAccessFile file = new RandomAccessFile(fileName, "rw");
            file.seek(file.length());
            file.write(value.getBytes());
            file.writeChar('\n');
            Thread.sleep(1000);
        }
    }
}
```

Subclasses benefit from the `AbstractMonitor` class in that they don't have to rewrite the `startMonitoring(String filename)` method; they just have to worry about their own particular functionality for the `process()` method.

For example, let's write a subclass called `MemoryMonitor` that outputs the current time and CPU utilization:

```java
public class MemoryMonitor extends AbstractMonitor {

    @Override
    public String process() {
        return new Date() + ":" + Runtime.getRuntime().freeMemory();
    }

    public static void main(String[] args) throws IOException, InterruptedException {
        new MemoryMonitor().startMonitoring("test.txt");
    }
}
```