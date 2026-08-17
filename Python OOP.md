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


