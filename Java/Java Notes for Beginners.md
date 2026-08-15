A complete beginner-friendly reference covering all the core Java topics you need to know.

## 📑 Table of Contents

1. [[#1. Introduction to Java|Introduction to Java]]
2. [[#2. Basic Structure of a Java Program|Basic Structure of a Java Program]]
3. [[#3. Variables and Data Types|Variables and Data Types]]
4. [[#4. Operators|Operators]]
5. [[#5. Control Statements|Control Statements]]
6. [[#6. Arrays|Arrays]]
7. [[#7. Strings|Strings]]
8. [[#8. Object-Oriented Programming (OOP)|Object-Oriented Programming (OOP)]]
9. [[#9. Constructors|Constructors]]
10. [[#10. Access Modifiers|Access Modifiers]]
11. [[#11. Static and Final Keywords|Static and Final Keywords]]
12. [[#12. Exception Handling|Exception Handling]]
13. [[#13. Collections Framework|Collections Framework]]
14. [[#14. Wrapper Classes|Wrapper Classes]]
15. [[#15. Java Memory Stack vs Heap|Java Memory: Stack vs Heap]]
16. [[#16. Packages and Import|Packages and Import]]
17. [[#17. Input from User|Input from User]]
18. [[#18. Important Keywords Cheat Sheet|Important Keywords Cheat Sheet]]
19. [[#19. Common Beginner Mistakes to Avoid|Common Beginner Mistakes to Avoid]]
20. [[#20. Quick Practice Ideas|Quick Practice Ideas]]

---

## 1. Introduction to Java

- Java is a **high-level, object-oriented, platform-independent** programming language.
- Motto: **"Write Once, Run Anywhere" (WORA)** — possible because of the JVM.
- Created by **James Gosling** at Sun Microsystems (now owned by Oracle).

### JDK, JRE, JVM

|Term|Full Form|Purpose|
|---|---|---|
|JVM|Java Virtual Machine|Runs the compiled bytecode (`.class` files)|
|JRE|Java Runtime Environment|JVM + libraries needed to _run_ Java programs|
|JDK|Java Development Kit|JRE + compiler & tools needed to _develop_ Java programs|

---

## 2. Basic Structure of a Java Program

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

- `public class Main` — class name must match the file name (`Main.java`).
- `main` method — entry point of every Java application.
- `System.out.println()` — prints output with a new line.

---

## 3. Variables and Data Types

### Primitive Data Types

|Type|Size|Example|
|---|---|---|
|`byte`|1 byte|`byte b = 10;`|
|`short`|2 bytes|`short s = 100;`|
|`int`|4 bytes|`int a = 1000;`|
|`long`|8 bytes|`long l = 100000L;`|
|`float`|4 bytes|`float f = 5.5f;`|
|`double`|8 bytes|`double d = 5.55;`|
|`char`|2 bytes|`char c = 'A';`|
|`boolean`|1 bit|`boolean flag = true;`|

### Non-Primitive (Reference) Types

- `String`, Arrays, Classes, Interfaces

### Variable Declaration

```java
int age = 25;
String name = "John";
final double PI = 3.14; // constant
```

---

## 4. Operators

- **Arithmetic:** `+ - * / %`
- **Relational:** `== != > < >= <=`
- **Logical:** `&& || !`
- **Assignment:** `= += -= *= /=`
- **Increment/Decrement:** `++ --`
- **Ternary:** `condition ? value1 : value2`

```java
int result = (a > b) ? a : b;
```

---

## 5. Control Statements

### If-Else

```java
if (age >= 18) {
    System.out.println("Adult");
} else {
    System.out.println("Minor");
}
```

### Switch

```java
switch (day) {
    case 1: System.out.println("Monday"); break;
    case 2: System.out.println("Tuesday"); break;
    default: System.out.println("Invalid");
}
```

### Loops

```java
// for loop
for (int i = 0; i < 5; i++) { System.out.println(i); }

// while loop
int i = 0;
while (i < 5) { i++; }

// do-while loop
int j = 0;
do { j++; } while (j < 5);
```

### Break & Continue

- `break` — exits the loop.
- `continue` — skips current iteration.

---

## 6. Arrays

```java
int[] numbers = {1, 2, 3, 4, 5};
System.out.println(numbers[0]); // 1

// 2D Array
int[][] matrix = {{1, 2}, {3, 4}};
```

- Arrays have **fixed size** and are **zero-indexed**.
- `numbers.length` gives the size.

---

## 7. Strings

```java
String name = "Java";
name.length();        // length of string
name.charAt(0);        // character at index
name.substring(1, 3);  // substring
name.toUpperCase();    // uppercase
name.equals("Java");   // compare content
name.equalsIgnoreCase("java");
name + " Programming"; // concatenation
```

> Use `.equals()` to compare String content, **not `==`** (which compares references).

---

## 8. Object-Oriented Programming (OOP)

Java is based on 4 OOP pillars:

### a) Class and Object

```java
class Car {
    String color;
    void drive() {
        System.out.println("Driving...");
    }
}

Car myCar = new Car(); // object creation
myCar.color = "Red";
myCar.drive();
```

### b) Encapsulation

Wrapping data (variables) and methods together, using `private` fields with `public` getters/setters.

```java
class Person {
    private String name;
    public String getName() { return name; }
    public void setName(String n) { name = n; }
}
```

### c) Inheritance

```java
class Animal {
    void eat() { System.out.println("Eating"); }
}
class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}
```

### d) Polymorphism

- **Compile-time (Method Overloading):** Same method name, different parameters.

```java
void add(int a, int b) {}
void add(double a, double b) {}
```

- **Runtime (Method Overriding):** Subclass redefines parent method.

```java
class Animal { void sound() { System.out.println("Animal sound"); } }
class Cat extends Animal { void sound() { System.out.println("Meow"); } }
```

### e) Abstraction

- **Abstract class:**

```java
abstract class Shape {
    abstract void draw();
}
```

- **Interface:**

```java
interface Drawable {
    void draw();
}
```

---

## 9. Constructors

```java
class Student {
    String name;
    Student() { name = "Unknown"; }          // default constructor
    Student(String n) { name = n; }          // parameterized constructor
}
```

- `this` keyword refers to the current object.
- Constructors have the **same name as the class** and **no return type**.

---

## 10. Access Modifiers

|Modifier|Same Class|Same Package|Subclass|Everywhere|
|---|---|---|---|---|
|`private`|✅|❌|❌|❌|
|default (none)|✅|✅|❌|❌|
|`protected`|✅|✅|✅|❌|
|`public`|✅|✅|✅|✅|

---

## 11. Static and Final Keywords

- `static` — belongs to the class, not the object (shared across all instances).

```java
static int count = 0;
static void show() { }
```

- `final` —
    - `final variable` → constant (cannot change value)
    - `final method` → cannot be overridden
    - `final class` → cannot be inherited

---

## 12. Exception Handling

```java
try {
    int result = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());
} finally {
    System.out.println("Always executes");
}
```

- **Checked exceptions:** checked at compile time (e.g., `IOException`)
- **Unchecked exceptions:** checked at runtime (e.g., `NullPointerException`, `ArithmeticException`)
- `throw` — manually throw an exception.
- `throws` — declare exceptions a method might throw.

---

## 13. Collections Framework

|Interface|Implementation|Use Case|
|---|---|---|
|`List`|`ArrayList`, `LinkedList`|Ordered, allows duplicates|
|`Set`|`HashSet`, `TreeSet`|No duplicates|
|`Map`|`HashMap`, `TreeMap`|Key-value pairs|
|`Queue`|`LinkedList`, `PriorityQueue`|FIFO structure|

```java
List<String> list = new ArrayList<>();
list.add("A");
list.add("B");

Map<String, Integer> map = new HashMap<>();
map.put("Apple", 1);
map.get("Apple");
```

---

## 14. Wrapper Classes

Converts primitive types into objects.

|Primitive|Wrapper|
|---|---|
|int|Integer|
|double|Double|
|char|Character|
|boolean|Boolean|

```java
int a = 5;
Integer obj = a;   // autoboxing
int b = obj;       // unboxing
```

---

## 15. Java Memory: Stack vs Heap

- **Stack:** stores method calls and local variables (fast, short-lived).
- **Heap:** stores objects created using `new` (managed by Garbage Collector).

---

## 16. Packages and Import

```java
package com.myapp;
import java.util.Scanner;
```

- Package = folder-like structure to organize classes.
- `import` brings in classes from other packages.

---

## 17. Input from User

```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
System.out.print("Enter your name: ");
String name = sc.nextLine();
int age = sc.nextInt();
```

---

## 18. Important Keywords Cheat Sheet

|Keyword|Meaning|
|---|---|
|`new`|creates a new object|
|`this`|refers to current object|
|`super`|refers to parent class|
|`static`|class-level member|
|`final`|constant / non-overridable|
|`abstract`|incomplete class/method|
|`interface`|fully abstract type|
|`extends`|class inheritance|
|`implements`|interface implementation|
|`void`|method returns nothing|
|`null`|represents no value|

---

## 19. Common Beginner Mistakes to Avoid

- Comparing Strings using `==` instead of `.equals()`.
- Forgetting `break` in `switch` statements.
- Off-by-one errors in loops (`<=` vs `<`).
- Not initializing variables before use.
- Confusing `ArrayList` (dynamic) with array (fixed size).
- Forgetting `public static void main(String[] args)` exact signature.

---

## 20. Quick Practice Ideas

- Build a calculator using `switch`.
- Create a `Student` class with getters/setters and print details.
- Use `ArrayList` to store and sort a list of names.
- Write a program using inheritance (`Animal` → `Dog`, `Cat`).
- Handle exceptions in a simple divide program.

---

### 📌 Tip

Practice writing small programs daily — Java concepts stick best through hands-on coding, not just reading notes.