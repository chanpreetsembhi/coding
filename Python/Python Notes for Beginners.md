A complete beginner-friendly reference covering all the core Python topics you need to know.

## 📑 Table of Contents

1. [[#1. Introduction to Python|Introduction to Python]]
2. [[#2. Basic Structure of a Python Program|Basic Structure of a Python Program]]
3. [[#3. Variables and Data Types|Variables and Data Types]]
4. [[#Operators|Operators]]
5. [[#5. Control Statements|Control Statements]]
6. [[#6. Loops|Loops]]
7. [[#7. Strings|Strings]]
8. [[#8. Lists, Tuples, Sets|Lists, Tuples, Sets]]
9. [[#9. Dictionaries|Dictionaries]]
10. [[#10. Functions|Functions]]
11. [[#11. Object-Oriented Programming (OOP)|Object-Oriented Programming (OOP)]]
12. [[#12. Constructors (`__init__`)|Constructors (`__init__`)]]
13. [[#13. Inheritance and Polymorphism|Inheritance and Polymorphism]]
14. [[#14. Exception Handling|Exception Handling]]
15. [[#15. File Handling|File Handling]]
16. [[#16. Modules and Packages|Modules and Packages]]
17. [[#17. List Comprehensions|List Comprehensions]]
18. [[#18. Lambda Functions|Lambda Functions]]
19. [[#19. Important Built-in Functions|Important Built-in Functions]]
20. [[#20. Common Beginner Mistakes to Avoid|Common Beginner Mistakes to Avoid]]
21. [[#21. Quick Practice Ideas|Quick Practice Ideas]]

---

## 1. Introduction to Python

- Python is a **high-level, interpreted, dynamically-typed** programming language.
- Created by **Guido van Rossum**, first released in 1991.
- Known for simple, readable syntax — great for beginners.
- Used in web development, data science, AI/ML, automation, scripting, etc.

---

## 2. Basic Structure of a Python Program

```python
# This is a comment
print("Hello, World!")
```

- No semicolons needed to end a line.
- No need to declare a `main` function (though `if __name__ == "__main__":` is common practice).
- Indentation (spaces) defines code blocks — **not curly braces**.

```python
def main():
    print("Hello, World!")

if __name__ == "__main__":
    main()
```

---

## 3. Variables and Data Types

Python is **dynamically typed** — no need to declare a type.

```python
name = "John"       # str
age = 25             # int
price = 99.99         # float
is_active = True      # bool
data = None           # NoneType
```

### Checking Type

```python
type(age)          # <class 'int'>
```

### Type Conversion

```python
int("10")     # string to int
str(10)       # int to string
float("5.5")  # string to float
```

---

## 4. Operators

- **Arithmetic:** `+ - * / // % **`
    - `/` → float division, `//` → floor division, `**` → power
- **Comparison:** `== != > < >= <=`
- **Logical:** `and or not`
- **Assignment:** `= += -= *= /=`
- **Membership:** `in`, `not in`
- **Identity:** `is`, `is not`

```python
print(10 // 3)   # 3
print(10 % 3)    # 1
print(2 ** 3)    # 8
print(5 in [1, 5, 9])  # True
```

---

## 5. Control Statements

```python
age = 20

if age >= 18:
    print("Adult")
elif age >= 13:
    print("Teenager")
else:
    print("Child")
```

> Python uses `elif`, not `else if`.

---

## 6. Loops

### For Loop

```python
for i in range(5):     # 0 to 4
    print(i)

for item in ["a", "b", "c"]:
    print(item)
```

### While Loop

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

### Break, Continue, Pass

```python
for i in range(10):
    if i == 5:
        break        # exits loop
    if i % 2 == 0:
        continue     # skips this iteration
    pass             # does nothing (placeholder)
```

---

## 7. Strings

```python
name = "Python"

len(name)            # length
name.upper()         # uppercase
name.lower()          # lowercase
name[0]               # indexing → 'P'
name[0:3]             # slicing → 'Pyt'
name + " Rocks"       # concatenation
name * 2               # repetition → 'PythonPython'

f"My language is {name}"   # f-string formatting
```

- Strings are **immutable** in Python.

---

## 8. Lists, Tuples, Sets

### List (ordered, mutable, allows duplicates)

```python
fruits = ["apple", "banana", "cherry"]
fruits.append("mango")
fruits.remove("banana")
fruits[0]              # 'apple'
fruits.sort()
```

### Tuple (ordered, immutable)

```python
point = (10, 20)
point[0]    # 10
```

### Set (unordered, no duplicates)

```python
nums = {1, 2, 3, 3, 2}   # {1, 2, 3}
nums.add(4)
```

---

## 9. Dictionaries

Key-value pairs (like a `Map` in other languages).

```python
person = {
    "name": "John",
    "age": 25
}

person["name"]           # 'John'
person["email"] = "a@b.com"   # add new key
person.keys()
person.values()
person.items()

for key, value in person.items():
    print(key, value)
```

---

## 10. Functions

```python
def greet(name, greeting="Hello"):
    return f"{greeting}, {name}!"

print(greet("John"))               # Hello, John!
print(greet("Sara", "Hi"))          # Hi, Sara!
```

- Default parameters, keyword arguments, and `*args` / `**kwargs` are supported.

```python
def total(*args):
    return sum(args)

def show_info(**kwargs):
    for k, v in kwargs.items():
        print(k, v)
```

---

## 11. Object-Oriented Programming (OOP)

```python
class Car:
    def __init__(self, color):
        self.color = color

    def drive(self):
        print("Driving...")

my_car = Car("Red")
my_car.drive()
print(my_car.color)
```

- `self` refers to the current instance (like `this` in Java).
- No explicit access modifiers — convention: `_protected`, `__private`.

---

## 12. Constructors (`__init__`)

```python
class Student:
    def __init__(self, name="Unknown"):
        self.name = name

s1 = Student("Alice")
s2 = Student()   # uses default "Unknown"
```

---

## 13. Inheritance and Polymorphism

### Inheritance

```python
class Animal:
    def sound(self):
        print("Animal sound")

class Dog(Animal):
    def sound(self):     # overriding
        print("Bark")

d = Dog()
d.sound()   # Bark
```

### Polymorphism

```python
def make_sound(animal):
    animal.sound()

make_sound(Dog())     # works for any subclass of Animal
```

### super()

```python
class Dog(Animal):
    def __init__(self, name):
        super().__init__()
        self.name = name
```

---

## 14. Exception Handling

```python
try:
    result = 10 / 0
except ZeroDivisionError as e:
    print("Error:", e)
except Exception as e:
    print("Something went wrong:", e)
else:
    print("No errors occurred")
finally:
    print("Always executes")
```

- `raise` — manually throw an exception.

```python
raise ValueError("Invalid input")
```

---

## 15. File Handling

```python
# Writing to a file
with open("data.txt", "w") as f:
    f.write("Hello, File!")

# Reading a file
with open("data.txt", "r") as f:
    content = f.read()
    print(content)
```

- `with` automatically closes the file — preferred over manual `open()`/`close()`.
- Modes: `"r"` read, `"w"` write, `"a"` append, `"r+"` read/write.

---

## 16. Modules and Packages

```python
import math
print(math.sqrt(16))     # 4.0

from math import pi
print(pi)

import mymodule as mm    # custom module with alias
```

- A **package** is a folder containing multiple modules (with an `__init__.py` file).

---

## 17. List Comprehensions

A concise way to create lists.

```python
squares = [x**2 for x in range(5)]          # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```

---

## 18. Lambda Functions

Anonymous, single-expression functions.

```python
square = lambda x: x * x
print(square(5))    # 25

add = lambda a, b: a + b
print(add(2, 3))    # 5
```

Often used with `map()`, `filter()`, `sorted()`:

```python
nums = [1, 2, 3, 4]
doubled = list(map(lambda x: x * 2, nums))
evens = list(filter(lambda x: x % 2 == 0, nums))
```

---

## 19. Important Built-in Functions

|Function|Purpose|
|---|---|
|`print()`|output to console|
|`len()`|length of object|
|`type()`|type of object|
|`range()`|sequence of numbers|
|`input()`|get user input|
|`int()`, `str()`, `float()`|type conversion|
|`sorted()`|returns sorted list|
|`sum()`, `min()`, `max()`|numeric operations|
|`zip()`|combine iterables|
|`enumerate()`|index + value while looping|

```python
for i, value in enumerate(["a", "b", "c"]):
    print(i, value)
```

---

## 20. Common Beginner Mistakes to Avoid

- Mixing tabs and spaces for indentation (causes errors).
- Forgetting the colon `:` after `if`, `for`, `def`, etc.
- Using `=` instead of `==` for comparison.
- Modifying a list while iterating over it.
- Confusing mutable (`list`) vs immutable (`tuple`) types.
- Forgetting `self` as the first parameter in class methods.

---

## 21. Quick Practice Ideas

- Build a simple calculator using functions.
- Create a `Student` class with attributes and methods.
- Use a dictionary to store and look up contact info.
- Read a text file and count word frequency.
- Write a list comprehension to filter even numbers from a list.

---

### 📌 Tip

Practice writing small Python scripts daily — the syntax is simple, but fluency comes from writing real code, not just reading notes.