# Python Fundamentals & OOP Cheat Sheet 🚀

Welcome! This repository serves as a comprehensive reference guide covering **Python Basics**, **Object-Oriented Programming (OOP)**, and advanced features including File I/O, Multithreading, and API integration.

---

## 📚 Table of Contents

1. [Python Basics](#1-python-basics)
   * [Variables & Data Types](#variables--data-types)
   * [Typecasting & User Input](#typecasting--user-input)
   * [Arithmetic Operators & Math Module](#arithmetic-operators--math-module)
   * [Conditionals & Logical Operators](#conditionals--logical-operators)
   * [String Methods & Indexing](#string-methods--indexing)
   * [Loops (While & For)](#loops-while--for)
   * [Data Structures (Collections)](#data-structures-collections)
   * [Functions, *args & **kwargs](#functions-args--kwargs)
   * [Advanced Concepts (List Comprehension, Match-Case, Scope)](#advanced-concepts)
2. [Object-Oriented Programming (OOP)](#2-object-oriented-programming-oop)
   * [Classes & Objects](#classes--objects)
   * [Class Variables](#class-variables)
   * [Inheritance & `super()`](#inheritance--super)
   * [Polymorphism & Duck Typing](#polymorphism--duck-typing)
   * [Static & Class Methods](#static--class-methods)
   * [Magic (Dunder) Methods](#magic-dunder-methods)
   * [Decorators & `@property`](#decorators--property)
3. [Advanced Topics](#3-advanced-topics)
   * [Exception Handling](#exception-handling)
   * [File I/O (txt, json, csv)](#file-io-txt-json-csv)
   * [Multithreading](#multithreading)
   * [Working with APIs](#working-with-apis)

---

## 1. Python Basics

### Variables & Data Types
A variable is a container for storing data values.

```python
# Strings
first_name = "Ahmed"
food = "Pizza"

# Integers
age = 19
quantity = 3

# Floats
price = 10.99
gpa = 3.2

# Booleans
is_student = True
is_online = False
```

---

### Typecasting & User Input
* **Typecasting:** Converting a variable from one data type to another using `str()`, `int()`, `float()`, or `bool()`.
* **`input()`:** Prompts the user for input and always returns a string.

```python
name = input("Enter your name: ")
age = int(input("Enter your age: "))

print(f"Hello {name}, you are {age} years old!")
```

---

### Arithmetic Operators & Math Module

```python
# Augmented assignment operators
age += 1  # Equivalent to age = age + 1

# Built-in math functions
round(3.142423, 3) # 3.142
abs(-4)            # 4
pow(4, 3)          # 64
max(3, 5, 9)       # 9
min(3, 5, 9)       # 3

# Using the math module
import math

print(math.pi)
math.sqrt(4)   # 2.0
math.ceil(9.1)  # 10
math.floor(9.9) # 9
```

---

### Conditionals & Logical Operators
Control execution flow using `if`, `elif`, `else`, combined with logical operators (`and`, `or`, `not`).

```python
temp = 20
is_sunny = True

if temp > 28 and is_sunny:
    print("It's HOT & Sunny ☀️")
elif temp <= 0 or not is_sunny:
    print("It's Cold or Cloudy ☁️")
else:
    print("Nice weather! 😊")

# Conditional Expression (Ternary Operator)
x = 5
status = "Positive" if x > 0 else "Negative"
```

---

### String Methods & Indexing

```python
name = "Ahmed Adel"

len(name)                # Length of string
name.find(" ")           # First occurrence index
name.lower()             # Convert to lowercase
name.upper()             # Convert to uppercase
name.isdigit()           # Returns True if digits only
name.replace(" ", "_")   # Replace substrings

# Indexing & Slicing: [start : end : step]
credit_number = "1234-5678-9012-3456"
print(credit_number[0])       # '1'
print(credit_number[:4])      # '1234'
print(credit_number[-4:])     # '3456'
print(credit_number[::2])     # Every second character
```

---

### Loops (While & For)

```python
# While Loop (runs while condition is True)
num = 0
while num < 5:
    print(num)
    num += 1

# For Loop (iterates over a sequence or range)
for x in range(1, 6):
    print(x, end=" ")
```

---

### Data Structures (Collections)

| Type | Syntax | Characteristics |
| :--- | :--- | :--- |
| **List** | `[]` | Ordered, Mutable, Allows Duplicates |
| **Tuple** | `()` | Ordered, Immutable, Faster Performance |
| **Set** | `{}` | Unordered, Mutable, **No Duplicates** |
| **Dictionary** | `{k: v}` | Key-Value Pairs, Mutable, Unique Keys |

```python
# List
fruits = ["apple", "orange", "banana"]
fruits.append("coconut")

# Tuple
coordinates = (10, 20)

# Set
unique_numbers = {1, 2, 3, 3, 4}  # Result: {1, 2, 3, 4}

# Dictionary
capitals = {"USA": "Washington D.C.", "Egypt": "Cairo"}
print(capitals.get("Egypt"))
```

---

### Functions, *args & **kwargs

```python
def add(x, y):
    return x + y

# Keyword & Default Arguments
def get_phone(country=20, area=123, number=4567):
    return f"+{country}-{area}-{number}"

# *args (positional arguments tuple) & **kwargs (keyword arguments dict)
def shipping_label(*args, **kwargs):
    for arg in args:
        print(arg, end=" ")
    print()
    for key, value in kwargs.items():
        print(f"{key}: {value}")
```

---

### Advanced Concepts

```python
# List Comprehension: [expression for value in iterable if condition]
doubles = [x * 2 for x in range(1, 11)]
evens = [x for x in range(1, 11) if x % 2 == 0]

# Match-Case Statement (Python 3.10+)
def day_of_week(day):
    match day:
        case 1: return "Sunday"
        case 2: return "Monday"
        case _: return "Invalid day"

# Main Block Pattern
if __name__ == '__main__':
    print("Running script directly...")
```

---

## 2. Object-Oriented Programming (OOP)

### Classes & Objects

```python
class Car:
    def __init__(self, model, year, color):
        self.model = model
        self.year = year
        self.color = color

    def drive(self):
        print(f"You drive the {self.color} {self.model}")

car1 = Car("BMW", 2026, "Black")
car1.drive()
```

---

### Class Variables
Shared attributes among all instances of a class.

```python
class Student:
    class_year = 2024
    num_students = 0

    def __init__(self, name):
        self.name = name
        Student.num_students += 1
```

---

### Inheritance & `super()`

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def eat(self):
        print(f"{self.name} is eating")

# Single Inheritance
class Dog(Animal):
    def speak(self):
        print("WOOF!")

# Extending parent methods with super()
class Shape:
    def __init__(self, color):
        self.color = color

class Circle(Shape):
    def __init__(self, color, radius):
        super().__init__(color)
        self.radius = radius
```

---

### Polymorphism & Duck Typing

```python
# Duck Typing: "If it looks like a duck and quacks like a duck, it's a duck."
class Dog:
    def speak(self): print("WOOF!")

class Cat:
    def speak(self): print("MEOW!")

class Car:
    def speak(self): print("HONK!")

# Executes speak() as long as the object defines it
for item in [Dog(), Cat(), Car()]:
    item.speak()
```

---

### Static & Class Methods

```python
class Employee:
    def __init__(self, name):
        self.name = name

    # Instance Method
    def get_name(self):
        return self.name

    # Static Method (Utility function; no self or cls access)
    @staticmethod
    def is_valid_position(position):
        return position in ["Developer", "Manager"]

    # Class Method (Operates on the class itself)
    @classmethod
    def get_company_info(cls):
        return "Company XYZ"
```

---

### Magic (Dunder) Methods

```python
class Book:
    def __init__(self, title, pages):
        self.title = title
        self.pages = pages

    def __str__(self):
        return f"'{self.title}', {self.pages} pages"

    def __eq__(self, other):
        return self.title == other.title

    def __gt__(self, other):
        return self.pages > other.pages

book1 = Book("Python Basics", 200)
book2 = Book("Python Basics", 150)

print(book1)          # Triggers __str__
print(book1 == book2) # True (Triggers __eq__)
print(book1 > book2)  # True (Triggers __gt__)
```

---

### Decorators & `@property`

```python
# Decorator Function
def add_sprinkles(func):
    def wrapper(*args, **kwargs):
        print("*Adds sprinkles ✨*")
        func(*args, **kwargs)
    return wrapper

@add_sprinkles
def get_ice_cream():
    print("Here is your ice cream 🍦")

# Property Decorators (Getters, Setters, Deleters)
class Rectangle:
    def __init__(self, width):
        self._width = width

    @property
    def width(self):
        return self._width

    @width.setter
    def width(self, value):
        if value > 0:
            self._width = value
        else:
            print("Width must be positive")
```

---

## 3. Advanced Topics

### Exception Handling

```python
try:
    number = int(input("Enter a number: "))
    print(10 / number)
except ZeroDivisionError:
    print("Error: Cannot divide by zero!")
except ValueError:
    print("Error: Invalid input. Enter numbers only.")
finally:
    print("Execution completed.")
```

---

### File I/O (txt, json, csv)

```python
import csv
import json

employees = [["Name", "Age"], ["Ahmed", 20]]

# Writing to CSV
with open("data.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerows(employees)

# Reading from CSV
with open("data.csv", "r") as file:
    reader = csv.reader(file)
    for row in reader:
        print(row)
```

---

### Multithreading

```python
import threading
import time

def task(name, duration):
    time.sleep(duration)
    print(f"Task {name} completed")

t1 = threading.Thread(target=task, args=("A", 2))
t2 = threading.Thread(target=task, args=("B", 4))

t1.start()
t2.start()

t1.join()
t2.join()
```

---

### Working with APIs

```python
import requests

def get_pokemon(name):
    url = f"https://pokeapi.co/api/v2/pokemon/{name}"
    response = requests.get(url, verify=False)
    
    if response.status_code == 200:
        data = response.json()
        print(f"Name: {data['name'].capitalize()}, ID: {data['id']}")
    else:
        print("Failed to fetch data")

get_pokemon("pikachu")
```
