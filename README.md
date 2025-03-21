# 1) Why Do We Need to Use OOP? Some Major OOP Languages

We generally use computers to model real-life concepts, and doing this with OOP makes development significantly easier. OOP languages provide a **class structure**, which allows data and the functions that manipulate it to be combined into a single object. This makes coding more organized, efficient, and convenient.

There are four key benefits of OOP: **Encapsulation, Abstraction, Inheritance, and Polymorphism.**

#### Understanding OOP with an Example

To better understand OOP, let's compare it to a non-OOP language like **C**. Suppose we want to model a **car** in C. We can group all the car's data in a **struct** and create functions to manipulate this data. However, these functions are not tied to the struct itself. Every time we call a function, we must pass a reference to the struct and use long function names to specify what data is being modified.

In OOP, we can define functions **inside** a class, allowing them to operate directly on the object's data. These functions, called **methods**, can be accessed using an operator (usually `.`), and they already have access to the object's internal data.
 
**Example:**

- **C:** `driveCar(*car, …);`
- **Java:** `car.drive(...);`

#### Encapsulation

In C, there is no built-in mechanism to prevent direct modifications of internal values. For example, we could set `fuelAmount = -99`, which doesn't make sense. While we could manually check for invalid values in every function, this creates unnecessary complexity and increases the risk of errors.

OOP solves this problem using **encapsulation**. With **access modifiers**, we can restrict direct access to data. Typically, object data is marked **private**, and access is controlled through **getter** and **setter** methods. This ensures values like `fuelAmount` can never be set to an invalid number.

#### Abstraction and Inheritance

Many objects share similar characteristics. For example, all cars have **engines, brakes, and tires**. Instead of writing the same code repeatedly, OOP allows us to **abstract** the common parts and focus only on the differences. We can create a base **Car** class with all shared logic and extend it to define specific car models.

This is called **inheritance**, and it greatly improves efficiency. In our car example, about **90% of the code** will already be written in the base class, allowing us to create multiple car models with minimal effort.

#### Polymorphism

Additionally, since different car models share common functionality, we can **store them in a single container** and perform operations on them as a group. Instead of treating each model separately, we can refer to all of them as **Car** objects. This concept is called **polymorphism** and makes managing complex systems much easier.

#### Major OOP Languages

- **C++**
- **C#:**
- **Java:**
- **Kotlin**

# 2) Interface vs. Abstract Class

#### What is an Interface?

An **interface** is used to define a set of behaviors that a class **must** implement. It acts as a **contract**, ensuring that any class implementing the interface follows a specific structure.

- Interfaces **only** contain **method signatures** (without implementation).
- Any class that implements an interface **must** provide an implementation for all its methods.
- A class can **implement multiple** interfaces, which allows for greater flexibility.

**Example:**

```java
interface Drawable {
    void draw();
}
```

#### What is an Abstract Class?

An **abstract class** is used to define common **behavior and data** that multiple related classes can share. Unlike interfaces, an abstract class **can contain both**:

- **Abstract methods** (methods without implementation, to be defined in subclasses).
- **Concrete methods** (fully implemented methods).
- **Instance variables** (fields with different access modifiers like `private` or `protected`).

However, a class can **extend only one** abstract class, as Java does not support multiple inheritance.

**Example:**

```java
abstract class AbstractShape implements Drawable {
    protected String color;

    public abstract void calculateArea();

    public void printColor() {
        System.out.println("Color of the shape is: " + color);
    }
}
```

#### When to Use Which?

- Use an **interface** when you need to enforce a **set of behaviors** across multiple unrelated classes. Provides flexibility and allow multiple inheritance of behavior.
- Use an **abstract class** when you have a base class that **shares common logic and data** with its subclasses. Allows code reuse and define shared behavior for related objects.

```java
class Triangle extends AbstractShape {
    private double base, height;

    public Triangle(String color, double base, double height) {
        super(color);
        this.base = base;
        this.height = height;
    }

    @Override
    public void calculateArea() {
        double area = 0.5 * base * height;
        System.out.println("Area: " + area);
    }

    @Override
    public void draw() {
        System.out.println("Drawing a " + color + " Triangle");
    }
}
```

1. `Drawable` → **Interface** (defines a contract).
2. `AbstractShape` → **Abstract Class** (implements `Drawable` and provides shared logic).
3. `Triangle` → **Concrete Class** (extends `AbstractShape` and provides specific behavior).

# 3) Why we need equals and hashcode? When to override?

The **equals** method is used to check if two objects are equal. In Java, the normal behavior when using the **==** operator is to compare the memory references of objects. This can lead to unexpected behavior. To compare the actual content of the objects, we need to **override equals** method.

The **hashCode** method is used when we want to represent an object as a number. It's commonly used in data structures like **HashMap** and **HashSet**. These structures use the hash code to assign a unique index for efficient storage and retrieval of data. The main benefit of this method is that it reduces the time complexity for data access to **O(1)**, assuming no collisions occur.

If two objects are considered equal (based on the equals method), their hash codes must also be the same. This is an important principle. Therefore, if you override equals method, you must also **override hashCode** method to ensure consistency.

# 4) Diamond Problem in Java? How to fix it?

The Diamond Problem is a term used to describe an issue in object-oriented programming languages that **allow multiple inheritance.** It occurs when a class inherits from two classes (or interfaces) that both have the **same method**. This creates ambiguity for the class that inherits from them, as it’s unclear which method should be inherited.

In a diamond-shaped inheritance structure, you have two classes B and C that both inherit from a common base class A. Then, class D inherits from both B and C. The problem arises if B and C have overridden a method from A, and D has to decide which one to use.

Java solves this problem by **not supporting multiple inheritance** for classes to avoid the Diamond Problem. However, it allows multiple inheritance for interfaces. In Java, the programmer is responsible for handling the ambiguity by explicitly overriding the conflicting methods in the implementing class. If both interfaces have a method with the same signature, the class implementing both interfaces must provide its own implementation of that method.

# 5) Why we need Garbage Collector? How does it run?

In programming, we often need to create objects at runtime, but we may not know exactly which objects or how many will be created. In such cases, we use heap memory to dynamically allocate space for objects. In C, the **malloc** function is used for this. However, there's a problem: every memory allocated with malloc() needs to be freed using **free()**. It's the programmer's responsibility to ensure that memory is cleared when it’s no longer needed, whether at the end of the program or not. Failing to do so can lead to memory leaks.

In Java, this problem is handled by the **Garbage Collector**. When you write code in Java, you don’t need to worry about manually managing memory for objects. The Garbage Collector runs in the background, **periodically checking** which objects are no longer in use and freeing up their memory. This simplifies development and ensures that memory leaks are avoided, **reducing the risk of human error**.

# 6) Java "static" keyword usage?

The static keyword in Java is used when we want to make a variable, method, or block **belong to the class** rather than instances of the class. This means that static members are shared among all objects of the class.

For example, when you declare a static variable, it is common for all instances of the class to have the same value. If you modify this value in one instance, the change will be reflected in all other instances.

A static method can be **called without creating an instance** of the class. It can only access other static members (variables and methods) within the class. Static methods cannot access instance variables or methods.

For instance, in a math library, you might have a static constant like PI to represent the value of pi, shared across all instances of the class, or you can have a static method like sqrt() to calculate the square root of a number, which can be called without creating an object of the class. Static blocks are used for initialization code that only needs to run once when the class is first loaded into memory.

# 7) Immutability means? Where and why to use it?

Immutability means that once an object is created,**its state (data) cannot be changed**. In Java, you can make a class immutable by marking its fields as final and not providing setters or methods that modify the fields after the object is created.

For example, a String in Java is immutable. Once a string is created, you cannot change its value. Instead, any operation on a string creates a new string object.

We use immutability in situations where we want to ensure that objects' data cannot be altered after they are created. This is particularly useful in **multi-threaded** environments because immutable objects are thread-safe — no other thread can modify them, reducing the chance of bugs and inconsistencies.

Immutability is also important when we want to represent constant values or ensure that the data remains consistent and secure.

# 8) Composition and Aggregation in Java and differences?

Composition and Aggregation are both types of associations in object-oriented programming, representing relationships between objects, but they differ in terms of ownership and lifecycle.

Composition represents a **strong "has-a"** relationship and **implies ownership**. It means that one object contains another object and is responsible for its creation and destruction. When the parent object is destroyed, the child object is also destroyed. This represents a whole-part relationship. In this example, the room is **created by** the House and when the house is destroyed, the room is **destroyed as well.**

```java
class House {
    private Room room;

    public House() {
        this.room = new Room();
    }
}

class Room {
    //...
}
```

Aggregation represents a **weaker "has-a"** relationship and **does not imply ownership**. It means that one object contains another object, but the contained object can exist independently of the container object. The lifecycle of the objects involved is not tied together. In this example the Book onbject is **passed to** Library. When the Library is destroyed, the Book **outlive** the Library.

```java
class Library {
    private Book book; 

    public Library(Book book) {
        this.book = book; 
    }

}

class Book {
    //...
}
```

# 9) Cohesion and Coupling means and differences?
Cohesion refers to how closely **related** and **focused** the responsibilities of a single class or module are. A class or module with high cohesion has methods and properties that are highly related to each other, making the class easier to understand and maintain. In simple terms, it’s about keeping things tightly grouped that belong together. In programming **high cohesion is preffered**
- public class **Utils** → Low cohesion
- public class **FileHandler** → Medium cohesion
- public class **ImageHandler** → High cohesion

Coupling refers to how **dependent** one class or module is on another. When classes are **loosely coupled**, they can function **independently**, which makes the system more flexible and easier to modify. On the other hand, tightly coupled classes are more **dependent** on each other, meaning a change in one class might **require changes in another class**.

**Highly coupled**
```java
class PSQLDatabase {
    //...
    public void log(){
        //...
    }
}

class Logger {
    private PSQLDatabase psqlDatabse; 

    public Logger() {
        this.psqlDatabse = new PSQLDatabase() ; 
    }
}
```

**Loosely coupled**
```java
interface SQLDatabase{
    public void log();
}

class PSQLDatabase implements SQLDatabase{
    //...
    @Override
    public void log(){
        //...
    }
}

class MySQLDatabase implements SQLDatabase{
    //...
    @Override
    public void log(){
        //...
    }
}

class Logger {
    private SQLDatabase sqlDatabase; 

    //Either PSQL or MYSQL database can be used
    public Logger(SQLDatabase sqlDatabase) {
        this.sqlDatabase = sqlDatabase; 
    }
}
```

# 10) Heap and Stack means and differences?

In memory management, Heap and Stack are two different regions where data is stored.

**Stack Memory**: **Small** and **fast**. It stores **method calls**, **local variables**, and runtime data. Each method call creates a stack frame, and memory is **automatically freed when the method completes**.

Heap Memory: **Large** and **flexible**. **Objects** are stored here, and their lifetime is **independent** of method calls. Heap memory is managed by the **Garbage Collector**.

Differences:

- Stack is faster, while Heap is larger and more flexible.
- Stack is automatically managed, while Heap is cleared by the Garbage Collector.
- Stack is method-based, while Heap is object-based.

# 11) Exception means? Type of Exceptions?

In languages like C, which do not have built-in exception handling, errors must be handled manually using return codes or flags. For example, functions often return special values (like -1 or NULL) to indicate failure, and the programmer must check these values after every function call. This makes the code harder to read and maintain. Additionally, recovering from errors requires explicit handling, such as manually freeing resources before exiting, increasing the risk of memory leaks and undefined behavior.
In java this problem is solved by **Exception Handling**. An exception is an **unexpected event** that occurs during program execution, **disrupting the normal flow** of instructions. In Java, exceptions help handle errors in a controlled way instead of crashing the program. In java the exceptions handled in **Try-Catch** blocks. We write the code in try block as if nothing wrongs will happen, and if something wrong happens it will change its flow to catch block, in which we can check what went wrong and act accordingly.

Types of Exceptions:

- **Checked** Exceptions: These are exceptions that must be handled during compilation, using try-catch or throws.
- **Unchecked** Exceptions: These occur at runtime and do not need to be declared or handled explicitly.
- **Errors**: These represent serious system-level issues that should not be handled by the application.

# 12) How to summarize 'clean code' as short as possible?

The answer to this question lies in understanding **why we need clean code**. In programming, we rarely work alone. We **collaborate**, **review others' code**, and continue working on projects started by other developers. To make this process smooth, code must be **clean and easy to understand**.

### Clean code should have:

- Descriptive variable names that clearly explain their purpose.
- Keeping the blocks short, breaking the blocks into their own functions.
- Short, single-responsibility functions that do one thing well.
- Proper abstraction to avoid unnecessary complexity.
- Consistent formatting for readability.

### You can consider your code clean if:

1) You can understand it even after a year.
2) Your colleagues can quickly understand what it does.
3) Even someone with zero programming knowledge can get a general idea of its functionality just by following the flow.

# 13) What is the method of hiding in Java?

Method hiding in Java occurs when a subclass defines a method with the **same signature as a method in the parent class**. Unlike method overriding, method hiding is related to **static methods**. In method hiding, the method in the subclass does not override the method in the parent class; instead, it hides it.

When you call a hidden method, the version that gets called depends on the type of the reference (the class type) used to call the method, not the object type. This is different from method overriding, where the method from the actual object is called.

For example, if you define a static method in both the parent and the subclass with the same name and parameters, the subclass method hides the parent method. The reference type decides which method is called.

# 14) What is the difference between abstraction and polymorphism in Java?


**Abstraction**: The concept of hiding complex implementation details and showing only the necessary features of an object. It is achieved using **abstract classes** or **interfaces**. The goal of abstraction is to reduce complexity by focusing on what an object does, rather than how it does it. For example, an abstract class or interface defines the structure that subclasses or implementing classes should follow.

**Polymorphism**: The ability of an object to take many forms. It allows one object to be treated as different types based on context, typically through method **overriding** or method **overloading**. This enables methods to be used interchangeably, even if they are defined in different classes.

**Abstraction**
```java
interface Drawable{
    //...
}

abstract class Shape implements Drawable{
    //...
}

class Quadrilateral extends AbstractShape{
    //...
}

class Rectangle extends Quadrilateral{
    //...
}

class Square extends Rectangle{
    //...
}
```

**Polymorphism**
```java
public void drawShapes(){
    List<Shape> shapes = new ArrayList<>();
    shapes.add(new Square(2));
    shapes.add(new Triangle(3,4,5));
    shapes.add(new Circle(1));
    shapes.add(new Hexagon(3,3,3,3,3,3));

    foreach(Shape shape : shapes){
        shape.draw();
    }
}
```