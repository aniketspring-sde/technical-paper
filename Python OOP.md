# Object-Oriented Programming in Python
### OOP is a programming paradigm in which software is organized around objects that combine state and behavior. It helps improve modularity, reuse, maintainability, and abstraction.
Main benefits of OOP:

1. **Modularity** — functionality is divided into classes.
2. **Reusability** — classes and components can be reused.
3. **Maintainability** — changes can be localized.
4. **Encapsulation** — implementation details can be hidden behind methods/properties.
5. **Extensibility** — inheritance, composition, and polymorphism allow systems to grow.
6. **Testability** — components can often be tested independently.

## Procedural programming is a programming paradigm where a program is organized as a sequence of procedures/functions that operate on data.
It focuses on step-by-step instructions to solve a problem, such as in C.

### Procedural vs OOP

| Procedural | OOP |
|---|---|
| Functions operate on data | Objects combine data and behavior |
| Often focuses on sequence of operations | Focuses on entities and responsibilities |
| Reuse through functions/modules | Reuse through composition/inheritance |
| Can become difficult to manage as state grows | State is associated with objects |
| Examples: C-style procedural programs | Python, Java, C++ support OOP |

**Important:** Python supports both procedural and object-oriented programming. Python is not exclusively an OOP language.

## A2. Classes and Objects
### Class

A class defines the structure and behavior that its instances can have.

```python
class Dog:
    pass
```
### Object

An object is a concrete instance of a class.

```python
d1 = Dog()
d2 = Dog()
```

`d1` and `d2` are different objects.

```python
print(d1 is d2)
# False
```
> A class is like a house blueprint. An object is an actual house built from that blueprint.


## A3. What is `self`?

`self` refers to the current instance.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def show(self):
        print(self.name)


s1 = Student("Aniket")
s1.show()
```

Conceptually, this:

```python
s1.show()
```

is similar to:

```python
Student.show(s1)
```

Therefore:

```python
def show(self):
```

needs `self` because Python passes the instance to the method.

### Important points

- `self` is a convention, not a reserved keyword.
- You could technically call it another name, but you should always use `self`.
- `self.name` means the `name` attribute belonging to the current instance.

---

## A4. Object creation: `__new__` vs `__init__`

When we write:

```python
d = Dog("Rex", 3)
```

Python internally performs:

```python
d = Dog.__new__(Dog, "Rex", 3)
Dog.__init__(d, "Rex", 3)
```

The exact call mechanics include arguments passed to `__new__`, but the key conceptual sequence is:

1. `__new__` creates the object.
2. `__init__` initializes the object.

### `__new__`

```python
class Demo:
    def __new__(cls):
        print("__new__ called")
        return super().__new__(cls)

    def __init__(self):
        print("__init__ called")


d = Demo()
```

Output:

```text
__new__ called
__init__ called
```

### `__init__`

`__init__` should initialize an already-created instance.

It should not return a different object.

```python
class Demo:
    def __init__(self):
        return 10
```

This raises `TypeError`.

> `__new__` is responsible for creating and returning an instance, while `__init__` initializes that instance after it has been created.

---

# THE FOUR PILLARS OF OOP

The four pillars are:

1. Encapsulation
2. Abstraction
3. Inheritance
4. Polymorphism


# ENCAPSULATION

## What is encapsulation?

Encapsulation means:

 Bundling data and the operations that work on that data together, while controlling how the internal state is accessed or modified.

Example:

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def deposit(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        self.__balance += amount

    def withdraw(self, amount):
        if amount <= 0:
            raise ValueError("Amount must be positive")

        if amount > self.__balance:
            raise ValueError("Insufficient balance")

        self.__balance -= amount

    def get_balance(self):
        return self.__balance
```
Usage:

```python
account = BankAccount(1000)

account.deposit(500)
account.withdraw(200)

print(account.get_balance())
```

The class controls how the balance changes.

---


## Python access modifiers

Python does not have Java-style compiler-enforced private fields.

| Syntax | Meaning |
|---|---|
| `name` | Public |
| `_name` | Internal/protected-by-convention |
| `__name` | Name-mangled |
| `__name__` | Dunder/special method naming |

### Single underscore

```python
class User:
    def __init__(self):
        self._password = "secret"
```

This does **not** prevent access.

```python
u = User()
print(u._password)
```

It communicates:

> "This is an internal implementation detail; external code should generally not depend on it."

### Double underscore

```python
class User:
    def __init__(self):
        self.__password = "secret"
```

Python name-mangles it approximately as:

```python
_User__password
```

Therefore:

```python
u = User()

print(u._User__password)
```

can still access it.

> `__private` does not mean true security/privacy. It primarily provides name mangling to avoid accidental name collisions, especially in inheritance.

# ABSTRACTION

## What is abstraction?

Abstraction means:

> Expose what an object can do while hiding unnecessary implementation details.

Example:

```python
class Car:
    def start(self):
        self._check_engine()
        self._inject_fuel()
        self._ignite()

        print("Car started")

    def _check_engine(self):
        pass

    def _inject_fuel(self):
        pass

    def _ignite(self):
        pass
```

The user only needs:

```python
car = Car()
car.start()
```

They do not need to know every internal operation.

---
## Abstract Base Classes

Python provides `abc`.

```python
from abc import ABC, abstractmethod


class Shape(ABC):

    @abstractmethod
    def area(self):
        pass

    @abstractmethod
    def perimeter(self):
        pass
```

A subclass must implement the abstract methods before it can be instantiated:

```python
class Rectangle(Shape):

    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

    def perimeter(self):
        return 2 * (self.length + self.width)
```

Now:

```python
r = Rectangle(10, 5)

print(r.area())
print(r.perimeter())
```

But:

```python
Shape()
```

raises a `TypeError`.

---

# INHERITANCE

## What is inheritance?

Inheritance allows one class to derive behavior and attributes from another class.

```python
class Animal:
    def speak(self):
        return "Some sound"


class Dog(Animal):
    pass


dog = Dog()

print(dog.speak())
```

`Dog` inherits `speak()` from `Animal`.

---

## Why use inheritance?

Use inheritance when there is a genuine **IS-A** relationship.

```text
Dog IS-A Animal
Car IS-A Vehicle
Manager IS-A Employee
```

Do not use inheritance merely because one class happens to need some methods from another.

---

## Method overriding

A child class can provide a different implementation.

```python
class Animal:
    def speak(self):
        return "Some sound"


class Dog(Animal):
    def speak(self):
        return "Woof"


class Cat(Animal):
    def speak(self):
        return "Meow"
```

This is method overriding.

---

## super()

`super()` is used to delegate to the next implementation according to the MRO.

```python
class Animal:
    def __init__(self, name):
        self.name = name


class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```



`super()` does **not** simply mean "call my immediate parent."

In multiple inheritance it means:

> Continue lookup according to the Method Resolution Order.

---

## Types of inheritance

### 1. Single inheritance

```text
Animal
   |
  Dog
```

```python
class Animal:
    pass

class Dog(Animal):
    pass
```

### 2. Multilevel inheritance

```text
Animal
   |
  Dog
   |
 Puppy
```
### 3. Hierarchical inheritance

```text
        Animal
       /      \
     Dog      Cat
```

### 4. Multiple inheritance

```text
A       B
 \     /
   \ /
    C
```

```python
class C(A, B):
    pass
```

### 5. Hybrid inheritance

Combination of multiple inheritance structures.

---

# METHOD RESOLUTION ORDER (MRO)

## What is MRO?

MRO is the order in which Python searches classes when resolving methods and attributes.

Example:

```python
class A:
    def show(self):
        return "A"


class B(A):
    def show(self):
        return "B"


class C(A):
    def show(self):
        return "C"


class D(B, C):
    pass
```

Now:

```python
print(D.mro())
```

Conceptually:

```text
D -> B -> C -> A -> object
```

Therefore:

```python
print(D().show())
```

returns:

```text
B
```

---

## C3 linearization

Python uses **C3 linearization** to calculate MRO.

The ordering must preserve important consistency rules, including:

1. A class appears before its parents.
2. The declared parent order is respected.
3. The ordering remains monotonic.

You can inspect MRO using:

```python
D.mro()
```

or:

```python
D.__mro__
```

---

## B4.3 Diamond problem

```text
       A
      / \
     B   C
      \ /
       D
```

Both `B` and `C` inherit from `A`.

Python must decide which implementation to use.

```python
class A:
    def show(self):
        print("A")


class B(A):
    def show(self):
        print("B")


class C(A):
    def show(self):
        print("C")


class D(B, C):
    pass
```
MRO:

```text
D -> B -> C -> A -> object
```

So:

```python
D().show()
```

prints:

```text
B
```

# POLYMORPHISM

## What is polymorphism?

Poly = many  
Morph = forms

Polymorphism means:

> The same interface or operation can work with different types and produce type-specific behavior.

```python
class Bird:
    def move(self):
        return "Flying"


class Fish:
    def move(self):
        return "Swimming"


def move_animal(animal):
    print(animal.move())


move_animal(Bird())
move_animal(Fish())
```

The function does not care about the concrete class. It only requires the `move()` behavior.

---
## Polymorphism through overriding

```python
class Animal:
    def sound(self):
        pass


class Dog(Animal):
    def sound(self):
        return "Woof"


class Cat(Animal):
    def sound(self):
        return "Meow"
```

```python
animals = [Dog(), Cat()]

for animal in animals:
    print(animal.sound())
```

Same method call:

```python
animal.sound()
```

Different result.

---
## Operator overloading

Python allows classes to define behavior for operators through special methods.

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def __add__(self, other):
        return Point(
            self.x + other.x,
            self.y + other.y
        )
```

Now:

```python
p1 = Point(1, 2)
p2 = Point(3, 4)

p3 = p1 + p2
```

Python effectively calls:

```python
p1.__add__(p2)
```

---

# METHOD OVERLOADING VS OVERRIDING

## Method overriding

Python supports overriding.

```python
class Parent:
    def show(self):
        print("Parent")


class Child(Parent):
    def show(self):
        print("Child")
```

```python
Child().show()
```

Output:

```text
Child
```

---

## Method overloading

Python does not support traditional compile-time method overloading like Java/C++.

This does not create two methods:

```python
class Calculator:

    def add(self, a, b):
        return a + b

    def add(self, a, b, c):
        return a + b + c
```

The second definition replaces the first.

### Default arguments

```python
class Calculator:
    def add(self, a, b=0, c=0):
        return a + b + c
```

### `*args`

```python
class Calculator:
    def add(self, *args):
        return sum(args)
```
# INSTANCE VARIABLES AND CLASS VARIABLES

## Instance variables

Each object has its own value.

```python
class Employee:
    def __init__(self, name, salary):
        self.name = name
        self.salary = salary
```

```python
e1 = Employee("A", 50000)
e2 = Employee("B", 60000)
```

Changing:

```python
e1.salary = 70000
```

does not change `e2.salary`.


## Class variables

Class variables belong to the class and are normally shared.

```python
class Employee:
    company = "ABC"
```

```python
e1 = Employee()
e2 = Employee()

print(e1.company)
print(e2.company)
```

Both access the class attribute.

## Attribute lookup

When Python evaluates:

```python
obj.x
```

it performs attribute lookup involving the instance and its class/MRO.

A useful simplified mental model is:

```text
object instance attributes
        ↓
class attributes
        ↓
base classes according to MRO
```

Descriptors and special lookup rules make the full algorithm more complex, but this model is excellent for basic interviews.

## Class attribute shadowing

```python
class Employee:
    company = "ABC"


e1 = Employee()
e2 = Employee()

e1.company = "XYZ"
```

Now:

```python
print(e1.company)
# XYZ

print(e2.company)
# ABC

print(Employee.company)
# ABC
```

`e1.company = "XYZ"` creates an instance attribute.

It does not modify the class variable.


# INSTANCE, CLASS, AND STATIC METHODS

## Instance method

Uses `self`.

```python
class Student:
    def __init__(self, name):
        self.name = name

    def introduce(self):
        return f"I am {self.name}"
```

The method operates on an instance.

## Class method

Uses `cls`.

```python
class Student:
    school = "ABC"

    @classmethod
    def change_school(cls, name):
        cls.school = name
```

Call:

```python
Student.change_school("XYZ")
```

Class methods are useful for:

- Alternate constructors
- Factory methods
- Operations involving class-level state

## Static method

Does not receive `self` or `cls`.

```python
class MathUtils:

    @staticmethod
    def add(a, b):
        return a + b
```

```python
print(MathUtils.add(2, 3))
```

Use it when the function logically belongs to the class namespace but does not need object/class state.

## Comparison table

| Feature | Instance method | Class method | Static method |
|---|---|---|---|
| First parameter | `self` | `cls` | None |
| Access instance state | Yes | No | No |
| Access class state | Yes | Yes | No |
| Decorator | None | `@classmethod` | `@staticmethod` |
| Typical use | Object behavior | Alternate constructors/class state | Utility logic |


## Alternate constructor

```python
class Person:

    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name, birth_year):
        age = 2026 - birth_year
        return cls(name, age)
```

```python
p = Person.from_birth_year("Sam", 2000)
```

Why use `cls` instead of `Person`?

Because subclasses can inherit the class method and still construct the subclass correctly.


# MAGIC / DUNDER METHODS

## What are dunder methods?

"Dunder" means **double underscore**.

Examples:

```python
__init__
__str__
__repr__
__len__
__eq__
__add__
__getitem__
__iter__
__call__
```

They allow Python's built-in operations to interact with user-defined objects.

## `__str__`

Used for a human-readable representation.

```python
class User:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"User: {self.name}"
```

```python
u = User("Aniket")
print(u)
```

## operator methods

| Python operation | Special method |
|---|---|
| `a + b` | `__add__` |
| `a - b` | `__sub__` |
| `a * b` | `__mul__` |
| `a / b` | `__truediv__` |
| `a == b` | `__eq__` |
| `a < b` | `__lt__` |
| `a > b` | `__gt__` |
| `len(a)` | `__len__` |
| `a[i]` | `__getitem__` |
| `for x in a` | `__iter__` |
| `a()` | `__call__` |
| `str(a)` | `__str__` |
| `repr(a)` | `__repr__` |

---

## Example

```python
class Book:

    def __init__(self, title, pages):
        self.title = title
        self.pages = pages

    def __str__(self):
        return self.title

    def __repr__(self):
        return f"Book({self.title!r}, {self.pages})"

    def __len__(self):
        return self.pages

    def __eq__(self, other):
        return self.pages == other.pages

    def __lt__(self, other):
        return self.pages < other.pages

    def __call__(self):
        return f"Reading {self.title}"
```

# PROPERTIES

## Why properties?

Suppose we want:

```python
user.age
```

but also want validation.

A property allows attribute-like syntax while executing logic.

```python
class Person:

    def __init__(self, age):
        self._age = age

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value < 0:
            raise ValueError("Age cannot be negative")

        self._age = value
```

Usage:

```python
p = Person(25)

print(p.age)

p.age = 30
```

## Read-only property

```python
class Circle:

    def __init__(self, radius):
        self.radius = radius

    @property
    def area(self):
        return 3.14159 * self.radius ** 2
```

Now:

```python
circle = Circle(5)

print(circle.area)
```

No setter means the property is effectively read-only through normal assignment.


# COMPOSITION VS INHERITANCE

## Inheritance = IS-A

```python
class Vehicle:
    pass


class Car(Vehicle):
    pass
```

A car **is a** vehicle.

---

## Composition = HAS-A

```python
class Engine:
    def start(self):
        return "Engine started"


class Car:

    def __init__(self):
        self.engine = Engine()

    def start(self):
        return self.engine.start()
```

A car **has an** engine.

---

## Why composition is often preferred

Inheritance creates stronger coupling.

Composition lets us replace components more easily.

For example:

```python
class DieselEngine:
    def start(self):
        return "Diesel engine started"


class ElectricEngine:
    def start(self):
        return "Electric motor started"


class Car:
    def __init__(self, engine):
        self.engine = engine

    def start(self):
        return self.engine.start()
```

Now:

```python
car1 = Car(DieselEngine())
car2 = Car(ElectricEngine())
```

The `Car` does not need to inherit from every possible engine type.


> Prefer composition over inheritance when the relationship is HAS-A rather than IS-A, or when composition provides better flexibility and lower coupling.


# ABSTRACT CLASS VS PROTOCOL

## I1. ABC

```python
from abc import ABC, abstractmethod


class PaymentProcessor(ABC):

    @abstractmethod
    def pay(self, amount):
        pass
```

Subclass:

```python
class UPIProcessor(PaymentProcessor):

    def pay(self, amount):
        return f"Paid {amount} using UPI"
```

This uses **nominal typing**: the class explicitly participates in the hierarchy.

