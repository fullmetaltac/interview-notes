# Table of Contents
- [Table of Contents](#table-of-contents)
  - [General](#general)
    - [What is Boxing and Unboxing?](#what-is-boxing-and-unboxing)
  - [Boxing allocates memory on the heap and can negatively impact performance if overused.](#boxing-allocates-memory-on-the-heap-and-can-negatively-impact-performance-if-overused)
    - [What is the difference between ref and out?](#what-is-the-difference-between-ref-and-out)
    - [What does the using keyword do?](#what-does-the-using-keyword-do)
    - [What is the difference between a method and a function in C#?](#what-is-the-difference-between-a-method-and-a-function-in-c)
    - [What is the difference between a value type and a reference type in C#?](#what-is-the-difference-between-a-value-type-and-a-reference-type-in-c)
    - [Can you explain the use of the "this" keyword in C#?](#can-you-explain-the-use-of-the-this-keyword-in-c)
    - [Can you explain the difference between a static and an instance method in C#?](#can-you-explain-the-difference-between-a-static-and-an-instance-method-in-c)
    - [What is a generic type in C# and why is it used?](#what-is-a-generic-type-in-c-and-why-is-it-used)
    - [What is an extension method in C# and how is it implemented?](#what-is-an-extension-method-in-c-and-how-is-it-implemented)
    - [Can you explain the difference between a method and an operator in C#?](#can-you-explain-the-difference-between-a-method-and-an-operator-in-c)
    - [Can you explain the difference between lazy and eager evaluation in C#?](#can-you-explain-the-difference-between-lazy-and-eager-evaluation-in-c)
    - [Explain the use of reflection in C#?](#explain-the-use-of-reflection-in-c)
    - [Explain the ?? operator and what is the correct way to use it in your code?](#explain-the--operator-and-what-is-the-correct-way-to-use-it-in-your-code)
    - [Can you explain the use of the as operator in C# and the best way to use it?](#can-you-explain-the-use-of-the-as-operator-in-c-and-the-best-way-to-use-it)
    - [Can you demonstrate how you would use a bitwise operator in C#?](#can-you-demonstrate-how-you-would-use-a-bitwise-operator-in-c)
    - [What is the difference between IEnumerable and IQueryable?](#what-is-the-difference-between-ienumerable-and-iqueryable)
  - [Object oriented programming](#object-oriented-programming)
    - [What is object-oriented programming?](#what-is-object-oriented-programming)
    - [What is a sealed class in C# and why is it used?](#what-is-a-sealed-class-in-c-and-why-is-it-used)
    - [What is an abstract class in C# and when is it used?](#what-is-an-abstract-class-in-c-and-when-is-it-used)
    - [What is an interface in C# and what is its purpose?](#what-is-an-interface-in-c-and-what-is-its-purpose)
    - [Can you explain the difference between an abstract class and an interface in C#?](#can-you-explain-the-difference-between-an-abstract-class-and-an-interface-in-c)
    - [What is a constructor in C# and what are its different types?](#what-is-a-constructor-in-c-and-what-are-its-different-types)
    - [What is the purpose of the base keyword in C#?](#what-is-the-purpose-of-the-base-keyword-in-c)
    - [How can you use the "base" keyword in C# to call the base class constructor?](#how-can-you-use-the-base-keyword-in-c-to-call-the-base-class-constructor)
    - [Can you discuss the differences between virtual methods and abstract methods in C#](#can-you-discuss-the-differences-between-virtual-methods-and-abstract-methods-in-c)
    - [How can you use inheritance and polymorphism together to achieve dynamic dispatch in C#?](#how-can-you-use-inheritance-and-polymorphism-together-to-achieve-dynamic-dispatch-in-c)
  - [LINQ](#linq)
    - [What is LINQ in C# and what is its purpose?](#what-is-linq-in-c-and-what-is-its-purpose)
    - [Can you explain the difference between a query expression and a method chain in LINQ?](#can-you-explain-the-difference-between-a-query-expression-and-a-method-chain-in-linq)
    - [How can LINQ be used to perform grouping and aggregation operations on data?](#how-can-linq-be-used-to-perform-grouping-and-aggregation-operations-on-data)
  - [Events](#events)
    - [What is a delegate in C# and how is it used?](#what-is-a-delegate-in-c-and-how-is-it-used)
    - [What is an event in C# and how is it different from a delegate?](#what-is-an-event-in-c-and-how-is-it-different-from-a-delegate)
    - [How can you subscribe and unsubscribe to an event in C#?](#how-can-you-subscribe-and-unsubscribe-to-an-event-in-c)
    - [What is an anonymous method in C# and how is it used?](#what-is-an-anonymous-method-in-c-and-how-is-it-used)
  - [Concurrency and Asynchronous Programming](#concurrency-and-asynchronous-programming)
    - [What is async/await?](#what-is-asyncawait)
    - [What is the difference between Task and Thread?](#what-is-the-difference-between-task-and-thread)
    - [What is a coroutine in C#?](#what-is-a-coroutine-in-c)
  - [References](#references)


## General

### What is Boxing and Unboxing?
Boxing is the process of converting a value type (e.g., int) to a reference type (object).
Unboxing is the reverse: extracting the value type from the object.

```cs
int x = 10;
object obj = x;       // Boxing
int y = (int)obj;     // Unboxing
```
Boxing allocates memory on the heap and can negatively impact performance if overused.
---

### What is the difference between ref and out?

| Feature                     | `ref`    | `out`        |
| --------------------------- | -------- | ------------ |
| Initialization before use   | Required | Not required |
| Must assign value in method | Optional | Required     |


```cs
void Test(ref int a, out int b) {
    a += 1;
    b = 10;
}
```

- `ref` allows a method to read and modify an already initialized variable.

- `out` is used to return multiple values; the variable must be assigned inside the method.

---

### What does the using keyword do?

Automatically disposes of resources (implements `IDisposable`) when the scope ends.

```cs
using (var file = new FileStream("test.txt", FileMode.Open)) {
    // File is automatically closed when block ends
}
```

### What is the difference between a method and a function in C#?

In C#, both methods and functions are terms used to describe executable code blocks that can be called to perform specific tasks. However, there's a subtle distinction between the two:

* **Method**: A method is a code block associated with a class or struct. It defines a set of instructions that can be executed on an instance of the class or struct, or it can be a static method that is associated with the class itself rather than instances of the class. Methods are used to perform actions, manipulate data, or provide functionality related to the class.

```cs
public class MathOperations
{
    public int Add(int a, int b)
    {
        return a + b;
    }
}

class Program
{
    static void Main(string[] args)
    {
        MathOperations math = new MathOperations();
        int result = math.Add(5, 3); // Calling the method
        Console.WriteLine(result);   // Output: 8
    }
}
```

* **Function**: In C#, the term "function" is commonly used interchangeably with "method." However, in a broader context, a function is a self-contained block of code that performs a specific task and can return a value. This term is often used in languages that support both procedural programming and object-oriented programming. Since C# is primarily an object-oriented language, the concept of "function" is usually referred to as "method."
---

### What is the difference between a value type and a reference type in C#?

In C#, data types are categorized into two main categories: value types and reference types. The distinction between these two types is crucial because it affects how data is stored and manipulated in memory.

* **Value Types**:  
  
Value types directly store the value itself, and they are usually stored in the stack memory. When you assign a value type to a new variable or pass it as a parameter to a method, a copy of the value is made. As a result, changes made to the copied value do not affect the original value.

```cs
// Numeric Types:
int x = 5;
int y = x; // y gets a copy of the value in x
y = 10;    // Changing y does not affect x
```

```cs
// Enumerations:
enum Color { Red, Green, Blue }
Color color1 = Color.Red;
Color color2 = color1; // color2 gets a copy of color1
color2 = Color.Green;  // Changing color2 does not affect color1
```

```cs
// Structures:
struct Point { public int X; public int Y; }
Point p1 = new Point { X = 2, Y = 3 };
Point p2 = p1;         // p2 gets a copy of p1
p2.X = 5;              // Changing p2 does not affect p1
```

* **Reference Types**:  
  
Reference types store a reference to the memory location where the data is actually stored, usually on the heap. When you assign a reference type to a new variable or pass it as a parameter to a method, you're passing a reference to the same memory location. This means changes made to the data are reflected wherever that data is referenced.

```cs
// Classes:
class Person { public string Name; }
Person person1 = new Person { Name = "Alice" };
Person person2 = person1;  // person2 references the same object as person1
person2.Name = "Bob";      // Changing person2 also changes person1
```
```cs
// Arrays:
int[] arr1 = new int[] { 1, 2, 3 };
int[] arr2 = arr1;      // arr2 references the same array as arr1
arr2[0] = 5;            // Changing arr2 also changes arr1
```
```cs
// Strings:
string str1 = "Hello";
string str2 = str1;     // str2 references the same string as str1
str2 = "Hi";            // Creates a new string object
```
---

### Can you explain the use of the "this" keyword in C#?

In C#, the "this" keyword is a reference to the current instance of a class or struct. It is commonly used to:

* Distinguish between instance variables and local variables with the same name.

```cs
class MyClass {
   int num;

   public void SetNum(int num) {
      this.num = num; // use "this" to refer to the instance variable
   }
}
```

* Pass the current object as an argument to another method or constructor. 

```cs
class MyClass {
   int num;

   public MyClass(int num) {
      this.num = num; // pass "this" as an argument to set the instance variable
   }

   public void DoSomething() {
      OtherClass.Method(this); // pass "this" as an argument to another method
   }
}
```

* Return the current object from a method. This is useful for chaining method calls.

```cs
class MyClass {
   public MyClass DoSomething() {
      // do something
      return this; // return the current object
   }

   public MyClass DoSomethingElse() {
      // do something else
      return this; // return the current object
   }
}
```
---

### Can you explain the difference between a static and an instance method in C#?

There are two types of methods in C#: static and instance methods.

* **Static Methods**: A static method is a method that is associated with the class rather than an instance of the class. It can be called without creating an instance of the class. In other words, it's a method that belongs to the type itself and not to an instance of the type.
```cs
public static int Add(int num1, int num2)
{
    return num1 + num2;
}
```
```cs
int sum = MyClass.Add(5, 10);
```
* **Instance Methods**: An instance method is a method that is associated with an instance of a class. It can only be called on an instance of the class, after an object of the class has been created.
```cs
public void DisplayMessage(string message)
{
    Console.WriteLine(message);
}
```
```cs
MyClass obj = new MyClass();
obj.DisplayMessage("Hello, world!");
```
---

### What is a generic type in C# and why is it used?

In C#, generic types are a feature that allows developers to define classes, interfaces, methods, or delegates with a placeholder for data types. Instead of specifying a concrete type, generics enable you to create more flexible, reusable, and type-safe code.

```cs
class Inventory<T> {
    private List<T> _items = new List<T>();

    public void AddItem(T item) {
        _items.Add(item);
    }

    public T GetItem(int index) {
        return _items[index];
    }
}
```
---

### What is an extension method in C# and how is it implemented?

An extension method in C# is a static method that allows you to extend the functionality of an existing type without modifying the type's original source code.

```cs
public static class StringExtensions
{
    public static string Reverse(this string str)
    {
        char[] charArray = str.ToCharArray();
        Array.Reverse(charArray);
        return new string(charArray);
    }
}
```
```cs
using ExtensionMethods;

string original = "Hello, world!";
string reversed = original.Reverse();

Console.WriteLine(reversed); // Outputs: "!dlrow ,olleH"
```
---

### Can you explain the difference between a method and an operator in C#?

In C#, both methods and operators are used to perform operations on data, but they differ in how they are defined and used.

* A method is a block of code that can be called by its name to perform a specific task. It can take input parameters, perform operations, and return a result. Methods are defined as part of a class, and they can be called on instances of that class or on the class itself.

```cs
public int Add(int a, int b)
{
    return a + b;
}
```
```cs
int result = Add(5, 10); // result will be 15
```

* An operator, on the other hand, is a special symbol or keyword that performs a specific operation on one or more operands. Operators are predefined in C# and can be used with built-in types, user-defined types, and enumerations.
```cs
int result = 5 + 10; // result will be 15
``` 

* Operators can also be overloaded, which means that you can define new behavior for an existing operator when it is used with your own types.
```cs
public static Vector operator +(Vector a, Vector b)
{
    return new Vector(a.X + b.X, a.Y + b.Y, a.Z + b.Z);
}
```
```cs
Vector result = vector1 + vector2;
```
---

### Can you explain the difference between lazy and eager evaluation in C#?

In C#, lazy evaluation and eager evaluation refer to two different approaches for evaluating expressions and handling computations.

* **Lazy evaluation**, also known as delayed evaluation, is an evaluation strategy where expressions are not evaluated until they are actually needed. This means that the computation is deferred until it is absolutely necessary, usually to avoid unnecessary calculations or to save resources. In C#, lazy evaluation is often implemented using a technique called "lazy loading," where the value of an expression is only computed the first time it is needed, and then cached for later use. Lazy evaluation can be useful when working with complex, resource-intensive calculations or when working with large data sets that may not all be needed at once.
```cs
Func<int> lazySum = () => x + y; // lazy evaluation, sum is not computed yet
int result = lazySum(); // the expression is evaluated when it is needed
```

* On the other hand, **eager evaluation**, also known as immediate evaluation, is the default evaluation strategy in C#. This means that expressions are evaluated as soon as they are encountered in the code, without any delay. This can be useful for simple or short-lived computations where the result is needed immediately, but it can also lead to unnecessary computation or resource consumption if the expressions are not carefully designed.
```cs
int x = 5;
int y = 10;
int sum = x + y; // eager evaluation, sum is computed immediately
```
---

### Explain the use of reflection in C#?

Reflection in C# is a powerful feature that allows you to inspect and interact with the metadata of types (classes, interfaces, etc.) at runtime. It provides a way to examine and manipulate the structure, behavior, and attributes of types, including accessing fields, properties, methods, and events dynamically.


**Common Use Cases of Reflection**:  

* **Dynamic Loading and Instantiation**: Reflection is often used when you need to dynamically load and instantiate types at runtime. For example, you might have a configuration file specifying a class name, and you want to create an instance of that class without knowing it at compile time.
```cs
string typeName = "Namespace.ClassName";
Type type = Type.GetType(typeName);
object instance = Activator.CreateInstance(type);
```

* **Accessing Members Dynamically**: Reflection allows you to access and invoke members (fields, properties, methods) of a type dynamically. This is useful when dealing with objects of unknown types.

```cs
Type type = typeof(MyClass);
PropertyInfo property = type.GetProperty("MyProperty");
object value = property.GetValue(myObject);
```

* **Attribute Inspection**: Reflection is commonly used for inspecting custom attributes applied to types or members. This can be useful in scenarios like custom serialization or validation.
```cs
Type type = typeof(MyClass);
var attributes = type.GetCustomAttributes(typeof(MyCustomAttribute), true);
```

**Appropriate Times to Use Reflection**:  

* **When Dealing with Unknown Types**: Use reflection when you need to work with types that are not known at compile time, such as loading plugins or implementing generic frameworks.

* **Metadata Inspection**: Use reflection when you need to inspect metadata, like attributes, or when building tools that analyze code.

* **Serialization and Deserialization**: Reflection is often used in serialization frameworks to dynamically inspect and manipulate object structures.

**Inappropriate Times to Use Reflection**:  

* **Performance-Critical Code**: Reflection can be slower compared to direct, compile-time code. Avoid using reflection in performance-critical sections of your application.

* **Security-Sensitive Scenarios**: Reflection can be a security risk, especially if it's used to access or modify private members of a type. It's important to validate and secure the use of reflection, especially in scenarios where security is crucial.

* **Code Maintainability**: Excessive use of reflection can make code less maintainable, as it may lead to hard-to-read and error-prone code. Favor strongly-typed code whenever possible.

---

### Explain the ?? operator and what is the correct way to use it in your code?

In C#, the `??` operator is called the null-coalescing operator. It is used for handling null values in expressions and provides a concise way to return a default value when a nullable type is null. The syntax is as follows:

```cs
result = expression1 ?? expression2;
```
```cs
// Example 1: Using ?? with nullable types
int? nullableValue = GetNullableValue(); // some method returning a nullable int

// If nullableValue is not null, result will be nullableValue; otherwise, it will be 10.
int result = nullableValue ?? 10;

// Example 2: Using ?? with reference types
string nullableString = GetString(); // some method returning a string or null

// If nullableString is not null, result will be nullableString; otherwise, it will be "Default".
string resultString = nullableString ?? "Default";
```
---

### Can you explain the use of the as operator in C# and the best way to use it?

In C#, the as operator is used for casting or converting a variable to a different type, but with a safer approach than some other casting operators. The as operator is particularly useful when you want to perform a cast, but you're not sure if the cast is valid. If the cast is not valid, the as operator returns null instead of throwing an exception.

```cs
object myObject = "Hello, World!";

// Attempt to cast using the as operator
string myString = myObject as string;

if (myString != null)
{
    Console.WriteLine("Casting successful: " + myString);
}
else
{
    Console.WriteLine("Casting failed");
}
```
---

### Can you demonstrate how you would use a bitwise operator in C#?

Bitwise operators manipulate individual bits within integral data types like integers (int), longs (long), bytes (byte), etc. They are primarily used in scenarios where you need to perform low-level bit manipulation or optimize storage.

```cs
using System;

class Program
{
    static void Main()
    {
        int num1 = 10;  // Binary: 1010
        int num2 = 6;   // Binary: 0110

        // Bitwise AND
        int resultAnd = num1 & num2;  // Binary: 0010 (2 in decimal)
        // Bitwise OR
        int resultOr = num1 | num2;   // Binary: 1110 (14 in decimal)
        // Bitwise XOR
        int resultXor = num1 ^ num2;  // Binary: 1100 (12 in decimal)
        // Bitwise NOT (Unary)
        int resultNot = ~num1;        // Binary: 0101 (in two's complement)
        // Bitwise Left Shift
        int resultLeftShift = num1 << 1;  // Binary: 10100 (20 in decimal)
        // Bitwise Right Shift
        int resultRightShift = num1 >> 1; // Binary: 0101 (5 in decimal)
    }
}
```

---

### What is the difference between IEnumerable and IQueryable?

| Feature      | `IEnumerable`      | `IQueryable`                |
| ------------ | ------------------ | --------------------------- |
| Execution    | In-memory          | Database-side (deferred)    |
| Suitable for | LINQ to Objects    | LINQ to Entities (e.g., EF) |
| Filtering    | After loading data | Translated to SQL query     |

- `IEnumerable` is best for in-memory collections.

- `IQueryable` builds expression trees and executes queries on the data source (e.g., SQL DB).

---

## Object oriented programming 

### What is object-oriented programming?

Object-Oriented Programming (OOP) is a programming paradigm that focuses on organizing code into objects, which are instances of classes. It promotes the idea of encapsulating data (attributes) and behavior (methods) related to a specific entity into a single unit. C# is a language that fully supports OOP concepts.

In C#, classes serve as blueprints for creating objects.

* **Class and Object Creation**: A class is a template that defines the structure and behavior of objects. An object is an instance of a class.
 
```cs
class Person
{
    public int Age;
    public string Name;

    public void Introduce()
    {
        Console.WriteLine($"Hi, I'm {Name} and I'm {Age} years old.");
    }
}

class Program
{
    static void Main()
    {
        Person person1 = new Person();
        person1.Name = "Alice";
        person1.Age = 30;
        person1.Introduce(); // Output: Hi, I'm Alice and I'm 30 years old.
    }
}
```

* **Encapsulation**: Encapsulation ensures that the internal details of an object are hidden from the outside world. It helps maintain data integrity and allows controlled access to data through methods.

```cs
class BankAccount
{
    private double balance;

    public void Deposit(double amount)
    {
        if (amount > 0)
            balance += amount;
    }

    public void Withdraw(double amount)
    {
        if (amount > 0 && amount <= balance)
            balance -= amount;
    }

    public double GetBalance()
    {
        return balance;
    }
}
```
* **Inheritance**: Inheritance allows you to create a new class based on an existing class, inheriting its attributes and methods. It promotes code reusability and hierarchy.

```cs
class Animal
{
    public string Species;

    public void MakeSound()
    {
        Console.WriteLine("Animal makes a sound.");
    }
}

class Dog : Animal
{
    public void Bark()
    {
        Console.WriteLine("Woof woof!");
    }
}
```

* **Polymorphism**: Polymorphism allows objects of different classes to be treated as objects of a common base class through inheritance. It enables dynamic method binding and flexibility in handling different object types.

```cs
class Shape
{
    public virtual void Draw()
    {
        Console.WriteLine("Drawing a shape.");
    }
}

class Circle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing a circle.");
    }
}

class Square : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing a square.");
    }
}
```

### What is a sealed class in C# and why is it used?

In C#, a sealed class is a class that cannot be inherited by other classes. When a class is marked as sealed, it means that it is complete and cannot be extended further.

The main reason to use a sealed class is to prevent the class from being modified or extended by other developers. This is useful when you want to ensure that the class works as intended and cannot be altered in unexpected ways. Sealed classes are also useful for performance reasons, as they can be optimized more effectively by the compiler.

```cs
sealed class MySealedClass
{
    // class members
}
```
---

### What is an abstract class in C# and when is it used?
In C#, an abstract class is a class that cannot be instantiated directly and must be inherited by a subclass. It is a way to provide a common interface and shared implementation for a group of related classes, while also allowing for individual implementation in each subclass.

An abstract class is defined using the abstract keyword before the class keyword. It can have abstract methods, which are declared without implementation, as well as non-abstract methods with implementation. Subclasses that inherit from the abstract class must implement all abstract methods or else they will also be abstract.

```cs
public abstract class Shape
{
    public abstract double GetArea();
    public abstract double GetPerimeter();
}

public class Rectangle : Shape
{
    private double length;
    private double width;
    
    public Rectangle(double length, double width)
    {
        this.length = length;
        this.width = width;
    }
    
    public override double GetArea()
    {
        return length * width;
    }
    
    public override double GetPerimeter()
    {
        return 2 * (length + width);
    }
}
```
---

### What is an interface in C# and what is its purpose?
In C#, an interface is a contract that defines a set of methods, properties, events, or indexers without implementing them. An interface does not contain any code for the behavior; it only specifies what can be done, not how it is done. Classes or structs that implement an interface are responsible for providing the concrete implementation for each member defined in the interface.

**Purpose of Interfaces in C#**  

The primary purpose of interfaces is to achieve abstraction and separation of concerns. Interfaces help in:

* **Defining a contract**: They force implementing classes to follow a certain structure, ensuring consistency across multiple types.
* **Loose coupling**: By depending on interfaces rather than concrete implementations, we reduce dependencies between parts of the code. This promotes better maintainability and flexibility.
* **Multiple inheritance**: C# does not support multiple class inheritance but allows a class to implement multiple interfaces.
* **Testability**: Interfaces make unit testing easier because they allow us to substitute real implementations with mock objects.

Let’s consider a scenario where we are designing a payment system for an e-commerce platform. The system needs to support multiple payment methods such as Credit Card, PayPal, and Bank Transfer.

```cs
public interface IPaymentProcessor
{
    void ProcessPayment(decimal amount);
    bool ValidatePaymentDetails();
}
```

```cs
public class CreditCardPaymentProcessor : IPaymentProcessor
{
    public void ProcessPayment(decimal amount)
    {
        Console.WriteLine($"Processing credit card payment of {amount}...");
        // Logic to process credit card payment
    }

    public bool ValidatePaymentDetails()
    {
        Console.WriteLine("Validating credit card details...");
        // Logic to validate credit card information
        return true;
    }
}
```
```cs
public class PayPalPaymentProcessor : IPaymentProcessor
{
    public void ProcessPayment(decimal amount)
    {
        Console.WriteLine($"Processing PayPal payment of {amount}...");
        // Logic to process PayPal payment
    }

    public bool ValidatePaymentDetails()
    {
        Console.WriteLine("Validating PayPal account...");
        // Logic to validate PayPal account
        return true;
    }
}
```
---

### Can you explain the difference between an abstract class and an interface in C#?

**Abstract Class:**  

An abstract class is a blueprint for other classes. It can contain both abstract members (without implementation) and concrete members (with implementation). Abstract classes serve as base classes and are used to provide common functionality to derived classes.

**Key Features:**  

* **Inheritance**: Supports single inheritance; a class can inherit from only one abstract class.
* **Members**: Can include fields, properties, methods, events, and constructors. Both abstract and concrete members are allowed.
* **Access Modifiers**: Members can have access modifiers (e.g., `public`, `protected`, `private`).
* **Purpose**: Used when there is a "is-a" relationship and shared implementation logic.

```cs
public abstract class Animal
{
    public abstract void MakeSound();

    public void Sleep()
    {
        Console.WriteLine("Sleeping...");
    }
}
```


**Interface:**  

An interface defines a contract for classes to implement. It contains only the signatures of methods, properties, events, or indexers without any implementation.

**Key Features:**  

* **Multiple Inheritance**: A class can implement multiple interfaces.
* **Members**: Cannot include fields or concrete members; all members are implicitly public and abstract.
* **Access Modifiers**: Members cannot have access modifiers; they are always public.
* **Purpose**: Used when there is a "can-do" relationship or when you want to define a strict contract.

```cs
public interface IAnimal
{
    void MakeSound();
    void Sleep();
}
```

**Key Differences**

| Feature              | Abstract Class                           | Interface                                  |
| -------------------- | ---------------------------------------- | ------------------------------------------ |
| **Implementation**   | Can include concrete methods and fields. | Cannot include concrete methods or fields. |
| **Inheritance**      | Single inheritance allowed.              | Multiple inheritance allowed.              |
| **Access Modifiers** | Members can have any access modifier.    | All members are implicitly `public`.       |
| **Constructors**     | Can have constructors.                   | Cannot have constructors.                  |
| **Usage Scenario**   | Use for shared behavior or base class.   | Use for defining a contract.               |

---

### What is a constructor in C# and what are its different types?

In C#, a constructor is a special method that is called when an object of a class is created. The purpose of a constructor is to initialize the state of an object with some initial values.

C# supports two types of constructors:

* **Instance Constructors**: An instance constructor is used to initialize the instance variables of a class. It is called when an object of the class is created using the new keyword. An instance constructor has the same name as the class and does not have a return type. Here is an example of an instance constructor:

```cs
public class MyClass {
    public int x;
    public int y;

    public MyClass(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

* **Static Constructors**: A static constructor is used to initialize the static variables of a class. It is called only once, when the class is first used. A static constructor has the same name as the class and does not have any parameters. Here is an example of a static constructor:

```cs
public class MyClass {
    public static int x;
    public static int y;

    static MyClass() {
        x = 10;
        y = 20;
    }
}
```

 > Note that a class can have multiple constructors, but they must have different signatures (i.e., different parameter lists). This is known as constructor overloading.

---

### What is the purpose of the base keyword in C#?

In C#, the base keyword is used to refer to the base class of the current class. It is used to access members of the base class, such as methods, properties, and fields.

```cs
public class Vehicle
{
    public int NumWheels { get; set; }

    public Vehicle(int numWheels)
    {
        NumWheels = numWheels;
    }
}

public class Car : Vehicle
{
    public string Make { get; set; }

    public Car(int numWheels, string make) : base(numWheels)
    {
        Make = make;
    }
}
```

---

### How can you use the "base" keyword in C# to call the base class constructor?

```cs
public class DerivedClass : BaseClass
{
    public DerivedClass(args)
    {
        base.MethodInBaseClass();
        int value = base.PropertyInBaseClass;
    }
}
```

---

### Can you discuss the differences between virtual methods and abstract methods in C#

* **Virtual Methods**: A virtual method is a method that can be overridden in a derived class. It provides a default implementation of a method that can be replaced with a derived class-specific implementation.
```cs
public class MyBaseClass
{
   public virtual void MyVirtualMethod()
   {
      Console.WriteLine("This is the base class virtual method.");
   }
}

public class MyDerivedClass : MyBaseClass
{
   public override void MyVirtualMethod()
   {
      Console.WriteLine("This is the derived class override of the virtual method.");
   }
}
```

* **Abstract Methods**: An abstract method is a method that does not have a default implementation in the base class and must be implemented by any derived class.
```cs
public abstract class MyBaseClass
{
   public abstract void MyAbstractMethod();
}

public class MyDerivedClass : MyBaseClass
{
   public override void MyAbstractMethod()
   {
      Console.WriteLine("This is the derived class implementation of the abstract method.");
   }
}
```


---


### How can you use inheritance and polymorphism together to achieve dynamic dispatch in C#?

In C#, inheritance and polymorphism can be used together to achieve dynamic dispatch through method overriding. Dynamic dispatch allows for the selection of the most appropriate method to be called based on the runtime type of the object.

```cs
public class Shape
{
    public virtual void Draw()
    {
        Console.WriteLine("Drawing a shape.");
    }
}
```
```cs
public class Circle : Shape
{
    public override void Draw()
    {
        Console.WriteLine("Drawing a circle.");
    }
}
```
```cs
Shape shape1 = new Shape();
Shape shape2 = new Circle();

shape1.Draw(); // Output: "Drawing a shape."
shape2.Draw(); // Output: "Drawing a circle."
```
This is an example of dynamic dispatch using inheritance and polymorphism in C#.

---






## LINQ

### What is LINQ in C# and what is its purpose?

LINQ (Language Integrated Query) is a feature of the C# programming language that provides a unified syntax for querying and manipulating data from various data sources such as collections, databases, XML documents, and more. LINQ allows developers to write queries using a familiar syntax that is similar to SQL, and it can be used with any data source that implements the IEnumerable or IQueryable interfaces.
```cs
var students = new List<Student>
{
    new Student { Name = "John", Age = 21, Grade = "A" },
    new Student { Name = "Mary", Age = 22, Grade = "B" },
    new Student { Name = "Jane", Age = 20, Grade = "A" }
};

var aStudents = students.Where(s => s.Grade == "A").ToList();
```
---

### Can you explain the difference between a query expression and a method chain in LINQ?

* A query expression is a declarative syntax for defining queries using a special set of keywords that are similar to those used in SQL. 
```cs
var query = from num in numbers
            where num % 2 == 0
            select num;
```
* A method chain, on the other hand, is an imperative syntax for defining queries using a series of extension methods that operate on an initial data source object. 
```cs
var query = numbers.Where(num => num % 2 == 0);
```

Both query expressions and method chains ultimately generate the same underlying code, so the choice between them often comes down to personal preference or readability.

---

### How can LINQ be used to perform grouping and aggregation operations on data?

* **Grouping Data**:  
  The GroupBy method in LINQ can be used to group data based on one or more properties. 
```cs
var products = new List<Product>
{
    new Product { Name = "Product1", Category = "Category1", Price = 10.00m },
    new Product { Name = "Product2", Category = "Category2", Price = 20.00m },
    new Product { Name = "Product3", Category = "Category1", Price = 30.00m },
    new Product { Name = "Product4", Category = "Category2", Price = 40.00m },
    new Product { Name = "Product5", Category = "Category1", Price = 50.00m }
};
```
```cs
var productsByCategory = products.GroupBy(p => p.Category);
```

* **Aggregating Data**:  
  Aggregation functions such as Sum, Min, Max, Average, and Count can be used to calculate summary information for a group of data.
```cs
var totalPricesByCategory = products
    .GroupBy(p => p.Category)
    .Select(g => new { Category = g.Key, TotalPrice = g.Sum(p => p.Price) });
```

---

## Events 

### What is a delegate in C# and how is it used?

In C#, a delegate is a type that represents a method with a specific signature. It can be used to reference a method and invoke it indirectly, which provides a flexible way of decoupling the caller from the callee.

A delegate declaration defines the signature of the method that it can reference. For example, the following delegate declaration defines a delegate type named MyDelegate that can reference a method that takes two integers as parameters and returns an integer:

```cs
delegate int MyDelegate(int x, int y);
```

A delegate object can be created by instantiating a delegate type with a method name or a lambda expression that matches the signature of the delegate type. For example, the following code creates a delegate object that references a method named Add
```cs
MyDelegate myDelegate = Add;
```
or with a lambda expression:
```cs
MyDelegate myDelegate = (x, y) => x + y;
```
Once a delegate object is created, it can be invoked like a method. The following code invokes the delegate object created above:
```cs
int result = myDelegate(1, 2); // result == 3
```

Delegates can also be used as event handlers in C# programs. When an event occurs, the delegate associated with the event is invoked, which can trigger the corresponding event handling code.

---

### What is an event in C# and how is it different from a delegate?

>**Delegates in C#**:  
  
A delegate is essentially a type-safe function pointer. It holds references to methods with a specific signature and return type, allowing methods to be passed as arguments or assigned to variables. Delegates enable dynamic method invocation, meaning that the methods they point to can be changed at runtime.

**Key Features of Delegates**:  

* **Type-Safety**: Delegates ensure that the methods they reference have the correct signature (input parameters and return type).
* **Multicasting**: A single delegate can reference multiple methods. When invoked, it calls each method in the order they were added.
* **Flexibility**: Delegates allow methods to be passed as parameters, useful for callback implementations, and facilitate decoupling of method logic from the caller.

```cs
public delegate void ProcessEvent(string message);

public class EventProcessor
{
    public void ProcessLog(string message)
    {
        Console.WriteLine($"Logging: {message}");
    }

    public void ProcessAlert(string message)
    {
        Console.WriteLine($"Alert: {message}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        EventProcessor processor = new EventProcessor();
        
        // Instantiate the delegate
        ProcessEvent processDelegate = processor.ProcessLog;
        
        // Multicast - add another method
        processDelegate += processor.ProcessAlert;

        // Invoke the delegate
        processDelegate("Critical system error");
    }
}
```

> Events in C#

An event is a specialized form of a delegate designed to enable safe and structured communication between objects, adhering to the publish-subscribe pattern. Events are used when one or more subscribers are interested in being notified when something occurs within a class.

**Key Features of Events**:

* **Encapsulation**: Unlike delegates, events add an additional layer of security by restricting the invocation of the event to the declaring class. Subscribers can only register or unregister from the event but cannot invoke it.
* **Publish-Subscribe Model**: Events allow objects to subscribe to specific events (e.g., when a button is clicked), and the event is raised when the triggering condition occurs.
* **Loose Coupling**: Events decouple the sender of the event from its subscribers. This means the class raising the event doesn’t need to know which specific methods will handle the event, which promotes a modular and maintainable design.

```cs
public delegate void Notify(string message);

public class Publisher
{
    // Declare the event using the delegate
    public event Notify OnPublishEvent;

    public void Publish(string message)
    {
        // Raise the event if there are subscribers
        OnPublishEvent?.Invoke(message);
    }
}

public class Subscriber
{
    public void HandleEvent(string message)
    {
        Console.WriteLine($"Subscriber received: {message}");
    }
}

class Program
{
    static void Main(string[] args)
    {
        Publisher publisher = new Publisher();
        Subscriber subscriber = new Subscriber();

        // Subscribe to the event
        publisher.OnPublishEvent += subscriber.HandleEvent;

        // Trigger the event
        publisher.Publish("New event occurred!");
    }
}
```
---



### How can you subscribe and unsubscribe to an event in C#?

In C#, you can subscribe to and unsubscribe from events using the event keyword and the += and -= operators, respectively.

```cs
// subscribe to the event
ExampleClass exampleObject = new ExampleClass();
exampleObject.MyEvent += HandleMyEvent;
```
```cs
// unsubscribe from the event
exampleObject.MyEvent -= HandleMyEvent;
```
---

### What is an anonymous method in C# and how is it used?

In C#, an anonymous method is a method that does not have a name and is defined inline within the code of another method or expression. It can be used in place of a named method anywhere a delegate is expected. A delegate is an object that can refer to a method and can be passed as a parameter or returned as a value.

Anonymous methods can be defined using the delegate keyword, followed by the argument list and body of the method. 

```cs
delegate (int x, int y) {
    return x + y;
};
```
```cs
int result = myDelegate(3, 4); // result = 7
```

Alternatively, C# also introduced lambda expressions, which are a shorter and more readable syntax for creating anonymous methods. For example, the anonymous method above can be expressed as a lambda expression like this:

```cs
(x, y) => x + y
```

Anonymous methods are commonly used in event handling and LINQ queries, among other places, where they allow for concise and flexible code.

---


## Concurrency and Asynchronous Programming

###  What is async/await?

`async` and `await` are used for asynchronous programming in C# to avoid blocking the main thread.

```cs
public async Task<string> GetDataAsync() {
    var response = await httpClient.GetStringAsync("https://api.com");
    return response;
}
```

- `async` marks a method as asynchronous.

- `await` pauses execution until the awaited task is complete.

- Great for I/O-bound tasks (web requests, file access).

---

### What is the difference between Task and Thread?

| Feature     | `Task`                        | `Thread`                     |
| ----------- | ----------------------------- | ---------------------------- |
| Abstraction | High-level                    | Low-level                    |
| Lightweight | Yes                           | No (more expensive)          |
| Managed by  | Task Scheduler (.NET runtime) | OS-level thread management   |
| Best for    | Asynchronous programming      | Long-running background work |

- `Task` is preferred for asynchronous operations, especially with `async/await`.

- `Thread` gives more control but is heavier and harder to manage.

---

### What is a coroutine in C#?

In C#, coroutines are a feature primarily used in Unity (a game engine built with C#) to allow execution of methods over multiple frames without blocking the main thread.

A coroutine is a special method that can pause its execution (yield) and resume later.

It is declared as a method that returns `IEnumerator` and uses `yield return` to control the execution flow.


```cs
IEnumerator WaitAndPrint() {
    yield return new WaitForSeconds(2f); // Wait for 2 seconds
    Debug.Log("Printed after delay");
}
```

You start a coroutine in Unity like this:

```cs
StartCoroutine(WaitAndPrint());
```

- Used for asynchronous behavior like delays, animations, or timed sequences.

- Not the same as `async/await` or multithreading.

- Runs on the main Unity thread, so it’s safe to interact with game objects.

---


## References
   - https://github.com/rcallaby/CSharp-Interview-Questions
    