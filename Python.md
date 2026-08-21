## Array methods
- arr = [1,2,3] 

| Method / Operation | Example | Result | Purpose |
|---|---|---|---|
| `append(x)` | `arr.append(10)` | `[1, 2, 3, 10]` | Add one item at end |
| `extend(iterable)` | `arr.extend([4, 5])` | `[1, 2, 3, 4, 5]` | Add multiple items |
| `insert(i, x)` | `arr.insert(1, 20)` | `[1, 20, 2, 3]` | Insert at index |
| `remove(x)` | `arr.remove(2)` | `[1, 3]` | Remove first matching item |
| `pop([i])` | `arr.pop()` | `3` | Remove and return item |
| `clear()` | `arr.clear()` | `[]` | Remove all items |
| `index(x)` | `arr.index(2)` | `1` | Find first index |
| `count(x)` | `arr.count(2)` | `1` | Count occurrences |
| `sort()` | `arr.sort()` | `[1, 2, 3]` | Sort in place |
| `reverse()` | `arr.reverse()` | `[3, 2, 1]` | Reverse in place |
| `copy()` | `arr2 = arr.copy()` | `[1, 2, 3]` | Shallow copy |

## String methods

str = "Hello"

| Method | Example | Result | Purpose |
|---|---|---|---|
| `lower()` | `str.lower()` | `"hello"` | Lowercase |
| `upper()` | `str.upper()` | `"HELLO"` | Uppercase |
| `strip()` | `str.strip()` | `"Hello"` | Remove surrounding whitespace |
| `replace()` | `str.replace('H', 'J')` | `"Jello"` | Replace substring |
| `split()` | `str.split('l')` | `['He', '', 'o']` | String → list |
| `join()` | `'-'.join(str)` | `"H-e-l-l-o"` | Iterable → string |
| `find()` | `str.find('ll')` | `2` | Index or `-1` |
| `index()` | `str.index('ll')` | `2` | Index or exception |
| `count()` | `str.count('l')` | `2` | Count substring |
| `startswith()` | `str.startswith('He')` | `True` | Prefix test |
| `endswith()` | `str.endswith('lo')` | `True` | Suffix test |
| `isdigit()` | `str.isdigit()` | `False` | Digit test |
| `isalpha()` | `str.isalpha()` | `True` | Alphabetic test |
| `isalnum()` | `str.isalnum()` | `True` | Alphanumeric test |

## Decorators

@staticmethod
- This decorator is used when we want to use a method without initializing a class object

  ```python
  class Calculator:

    @staticmethod    
    def add(a, b):    
       return a + b   
  
  print(Calculator.add(10, 20))


@classmethod
This is used to create a method that works with the class instead of an object instance. A class method receives the class itself as the first argument using cls. It is commonly used to access class variables, create factory methods, and perform operations related to the class.

```python
class Person:

    company = "ABC"

    @classmethod
    def show_company(cls):
        print(cls.company)

Person.show_company()
```

@property

This allows us to access a method like an attribute.
```python
class Person:

    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name


person = Person("Aniket")

print(person.name)
```
## virtualenv
- virtualenv is a tool used to create an isolated Python environment for a project. Instead of installing every Python package globally, you create a separate environment for each project.

     
  To create a virtual environment     
  python3 -m venv .venv    
  To activate the virtual environment     
  source (virtual_environment_name)/bin/activate        
  To deactivate the virtual environment    
  deactivate

## pip package manager
- pip is Python's standard package installer/package manager. It is used to install, upgrade, remove, and manage Python packages from the Python Package Index (PyPI) and other package repositories.

## PEP-8 standards summary

| Rule | Standard | Example |
|---|---|---|
| Indentation | Use 4 spaces | `print("Hello")` |
| Maximum line length | Prefer ≤ 79 characters | Keep long lines readable |
| Function naming | `snake_case` | `calculate_salary()` |
| Variable naming | `snake_case` | `employee_name` |
| Class naming | `PascalCase` | `EmployeeDetails` |
| Constant naming | `UPPER_CASE` | `MAX_SIZE = 100` |
| Module naming | Lowercase | `employee.py` |
| Package naming | Lowercase | `employee_data` |
| Function arguments | `snake_case` | `def add_numbers(a, b):` |
| Imports | One import per line | `import os` |
| Import order | Standard → Third-party → Local | See below |
| Blank lines | 2 around top-level functions/classes | Separate definitions |
| Spaces around operators | Use spaces | `x = a + b` |
| Spaces after commas | Use one space | `[1, 2, 3]` |
| Comments | Complete and clear | `# Calculate total salary` |
| Docstrings | Use for public functions/classes | `"""Calculate salary."""` |
| Comparisons | Use `is` for `None` | `if value is None:` |
| Boolean comparison | Avoid `== True` | `if is_valid:` |
