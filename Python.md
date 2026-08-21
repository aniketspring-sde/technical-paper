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


