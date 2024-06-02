# Python Prep work and main concepts

### Merging dictionaries
- unpacking into a new dict 
```python
{**dict1,**dict2}
```
- using the update method
```python
dict1.update(dict2)
```
- using the dict comprehension
```python
{key: value for d in [dict1, dict2] for key, value in d.items()}
```
- using the merge operator in Python 3.9
```python
dict1 | dict2
```
- But if we have duplicate keys, the last key will be the one that is kept.
- To avoid this, we can use the dict comprehension method to update the values into a list of both keys if needed.
```python
{key: [d[key] for d in [dict1, dict2] if key in d] for key in set(dict1) | set(dict2)}
```

### what are generators and yield ?
- Generators are iterators, but you can only iterate over them once. It’s because they do not store all the values in memory, they generate the values on the fly.
- You can create a generator function with `yield` instead of `return`.
- The `yield` keyword is used to return a value from a generator function.
- The generator function can pause and resume the function from where it left off.
- The generator function can also send a value back to the generator function.
- The generator function can also raise an exception.
- The generator function can also return a value.
- The generator function can also return a value with a return statement, but it will raise a `StopIteration` exception.

```python
def simple_gen():
    yield 1
    yield 2
    yield 3

gen = simple_gen()
print(next(gen)) # 1
print(next(gen)) # 2
print(next(gen)) # 3
print(next(gen)) # StopIteration
```

### Type checking variables in Python
- Python is a dynamically typed language, so the type of a variable is determined at runtime.
- But we can use the `typing` module to type check variables.
- We can use the `isinstance()` function to check the type of a variable.
- We can use the `mypy` tool to check the type of variables in our code.
- We can use the `@type` decorator to check the type of a function.
- We can use the `@overload` decorator to check the type of a function with multiple signatures. 


### Type hinting in Python
- Type hinting is a feature that allows us to specify the type of a variable in Python.
- We can use the `typing` module to specify the type of a variable.
- We can use the `mypy` tool to check the type of variables in our code.
- We can use the `@type` decorator to check the type of a function.
- We can use the `@overload` decorator to check the type of a function with multiple signatures.     
```python
from typing import overload
@overload
def add(a: int, b: int) -> int:
    ...
@overload
def add(a: float, b: float) -> float:
    ...
@overload
def add(a: str, b: str) -> str:
    ...
def add(a, b):
    return a + b
```

### Using the `@property` decorator in Python
- The `@property` decorator is used to define a property in a class.
- The `@property` decorator allows us to define a method that can be accessed as an attribute.
- The `@property` decorator is used to define a getter method.
- The `@property` decorator is used to define a setter method.
- The `@property` decorator is used to define a deleter method.
- The `@property.setter` decorator is used to define a setter method.
- The `@property.deleter` decorator is used to define a deleter method.
- The `@property` decorator is used to define a property with a getter, setter, and deleter method.
- The `@property` decorator is used to define a property with a getter and setter method.
- The `@property` decorator is used to define a property with a getter method.

```python
class Circle:
    def __init__(self, radius):
        self.radius = radius
    @property
    def area(self):
        return 3.14 * self.radius ** 2
    @property
    def perimeter(self):
        return 2 * 3.14 * self.radius
    @property
    def diameter(self):
        return 2 * self.radius

circle = Circle(5)
print(circle.area) # 78.5
print(circle.perimeter) # 31.400000000000002
print(circle.diameter) # 10
```

### Sets and methods in Python
- Sets are unordered collections of unique elements.
- Sets are mutable, so we can add or remove elements from a set.
- Sets are iterable, so we can loop over the elements in a set.
- Sets are unordered, so we cannot access elements in a set by index.

```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}
print(set1 | set2) # {1, 2, 3, 4, 5, 6, 7, 8}
print(set1 & set2) # {4, 5}
print(set1 - set2) # {1, 2, 3}
print(set1 ^ set2) # {1, 2, 3, 6, 7, 8}
```
```python
set1 = {1, 2, 3, 4, 5}
set2 = {4, 5, 6, 7, 8}

set3 = set1.difference(set2)
print(set3)  # {1, 2}
set1.difference_update(set2)
print(set1)  # {1, 2}

set4 = set1.intersection(set2)
print(set4)  # {4, 5}

is_disjoint = set1.isdisjoint(set2)
print(is_disjoint)  # False

is_subset = set1.issubset(set2)
print(is_subset)  # False

is_superset = set1.issuperset(set2)
print(is_superset)  # False

element = set1.pop()
print(element)  # 1

set1.remove(2)
print(set1)  # {}

set5 = set1.symmetric_difference(set2)
print(set5)  # {1, 2, 6, 7}

set6 = set1.union(set2)
print(set6)  # {1, 2, 4, 5, 6, 7, 8}
```
### Sorting based on the key descending
```python
k = dict(sorted(d.items(), key=lambda x: x[0], reverse=True))
```
### Sorting based on the value descending
```python
k = dict(sorted(d.items(), key=lambda x: x[1], reverse=True))
```

### what is assertion ?
- An assertion is a sanity check to make sure your code isn’t doing something obviously wrong.
- The `assert` statement is used to check if a condition is True.
- If the condition is False, the `assert` statement will raise an `AssertionError` exception.
- The `assert` statement can take an optional message to display when the condition is False.
- The `assert` statement can take multiple conditions separated by commas.
- The `assert` statement can take an expression that returns a value.

```python
x = 10
assert x == 10
assert x == 20, "x should be 20"
assert x == 30 and x == 40, "x should be 30 and 40"
assert x != "hello", "x should be 'hello'"
```

### LRU cache in Python
- The `functools` module provides a decorator called `lru_cache` that caches the result of a function.
- The `lru_cache` decorator caches the result of a function with a maximum size.
- The `lru_cache` decorator caches the result of a function with a maximum size and a time-to-live.

```python
from functools import lru_cache

@lru_cache(maxsize=128)
def fib(n):
    if n < 2:
        return n
    return fib(n - 1) + fib(n - 2)

print(fib(10))
print(fib(20))
print(fib(30))
```
### Caching Strategies in Python
| Strategy                    | Eviction policy                      | Use case                                      |
|-----------------------------|--------------------------------------|-----------------------------------------------|
| First-In/First-Out (FIFO)   | Evicts the oldest of the entries      | Newer entries are most likely to be reused    |
| Last-In/First-Out (LIFO)    | Evicts the latest of the entries      | Older entries are most likely to be reused    |
| Least Recently Used (LRU)   | Evicts the least recently used entry  | Recently used entries are most likely to be reused |
| Most Recently Used (MRU)    | Evicts the most recently used entry   | Least recently used entries are most likely to be reused |
| Least Frequently Used (LFU) | Evicts the least often accessed entry | Entries with a lot of hits are more likely to be reused |






### Using the `@staticmethod` decorator in Python
- The `@staticmethod` decorator is used to define a static method in a class.
- The `@staticmethod` decorator does not have access to the instance of the class.
- The `@staticmethod` decorator does not have access to the class itself.
- The `@staticmethod` decorator does not have access to the class attributes.
- The `@staticmethod` decorator does not have access to the instance attributes.
- The `@staticmethod` decorator is used to define a utility function in a class.
```python
class Circle:
    def __init__(self, radius):
        self.radius = radius
    
    @staticmethod
    def area(radius):
        return 3.14 * radius ** 2
    
    @staticmethod
    def perimeter(radius):
        return 2 * 3.14 * radius
    
    @staticmethod
    def diameter(radius):
        return 2 * radius

circle = Circle(5)
print(circle.area(5)) # 78.5
print(circle.perimeter(5)) # 31.400000000000002
print(circle.diameter(5)) # 10
```

### string to list and list to string
```python   
s = "hello"
l = list(s)
print(l) # ['h', 'e', 'l', 'l', 'o']
''.join(l) # hello
```

### lstrip, rstrip, strip and split methods
- lstrip() - Removes any leading characters
- rstrip() - Removes any trailing characters
- strip() - Removes any leading and trailing characters
- split() - Splits the string into a list of strings
- ltrip and rstrip can take a string as an argument to remove the leading or trailing characters.
-  

```python
s = " hello "
print(s.lstrip()) # 'hello '
print(s.rstrip()) # ' hello'
print(s.strip()) # 'hello'
print(s.split()) # ['hello']

s = "hello,world"
print(s.split(',')) # ['hello', 'world']

s = "abc.abc.abc.abc.world"
print(s.lstrip('abc.')) # 'world'
```

### User defined error handling
- We can create custom exceptions by inheriting from the `Exception` class.
- We can raise custom exceptions using the `raise` statement.
- We can catch custom exceptions using the `try` and `except` blocks.
- We can define an error message for custom exceptions.
- We can use the `finally` block to run cleanup code after the `try` and `except` blocks.
- We can use the `else` block to run code that should only run if there are no exceptions.

```python
class MyError(Exception):
    def __init__(self, message):
        self.message = message
        super().__init__(self.message)

try:
    raise MyError("This is a custom error")
except MyError as e:
    print(e)
finally:
    print("This is the finally block")
```
### ASCII and character conversion
- The `ord()` function returns the ASCII value of a character.
- The `chr()` function returns the character of an ASCII value.
```python
print(ord('a')) # 97
print(chr(97)) # a
```
### Shallow and deepcopy syntax and usage in Python
- The `copy` module provides the `copy` and `deepcopy` functions to create shallow and deep copies of objects.
- The `copy` function creates a shallow copy of an object.
- The `deepcopy` function creates a deep copy of an object.
- A shallow copy creates a new object, but does not create new objects for the nested objects.
- A deep copy creates a new object and creates new objects for the nested objects.
```python
from copy import copy, deepcopy

l1 = [1, 2, 3]
l2 = copy(l1)
l3 = deepcopy(l1)

l1[0] = 10
print(l1) # [10, 2, 3]
print(l2) # [1, 2, 3]
print(l3) # [1, 2, 3]
```
- Without using the `copy` module, we can use the slicing syntax to create a shallow copy of a list.
```python
l1 = [1, 2, 3]
l2 = l1[:]
l1[0] = 10
print(l1) # [10, 2, 3]
print(l2) # [1, 2, 3]
```

### Closure and scope in Python
- A closure is a function that captures the environment in which it was defined.
- In Python, closures grant nested functions read-only access to variables of the enclosing scope.
- A closure is a function that returns a function.

```python
def outer_func():
    message = "Hello"
    def inner_func():
        print(message)
    return inner_func
outer_func()()
```
### Typehinting in Python
- Type hinting is a feature that allows us to specify the type of a variable in Python.
- We can use the `typing` module to specify the type of a variable.

```python
from typing import List, Tuple, Dict, Any, Unio
def add(a: int, b: int) -> int:
    return a + b

def get_values(l: List[int]) -> Tuple[int]:
    return tuple(l)

def get_dict(a: int, b: int) -> Dict[str, Any]:
    return {"a": a, "b": b}

def get_value(a: int, b: int) -> Union[int, str]:
    if a == b:
        return a
    return "Not equal"
```
### API calling in Python
- We can use the `requests` module to make API calls in Python.
- We can use the `requests.get()` method to make a GET request.
- We can use the `requests.post()` method to make a POST request.
- We can use the `requests.put()` method to make a PUT request.
- We can use the `requests.delete()` method to make a DELETE request.
- We can use the `requests.patch()` method to make a PATCH request.
- We can use the `requests.head()` method to make a HEAD request.
- We can use the `requests.options()` method to make an OPTIONS request.
- We can use the `requests.request()` method to make a custom request.

```python   
import requests

response = requests.get("https://api.github.com")
print(response.status_code) # 200
print(response.json()) # {'current_user_url': 'https://api.github.com/user', 'current_user_authorizations_html_url': '
```

### bash executions in py scripts 
- We can use the `subprocess` module to execute bash commands in Python.
- We can use the `subprocess.run()` method to execute a bash command.
- We can use the `subprocess.Popen()` method to execute a bash command.
- We can use the `subprocess.check_output()` method to execute a bash command.
- We can use the `subprocess.call()` method to execute a bash command.
- We can use the `subprocess.check_call()` method to execute a bash command.
- We can use the `subprocess.check_output()` method to execute a bash command.
- We can use the `subprocess.check_output()` method to execute a bash command.

```python
import subprocess

subprocess.run("ls -l", shell=True)
subprocess.Popen("ls -l", shell=True)
subprocess.check_output("ls -l", shell=True)
subprocess.call("ls -l", shell=True)
subprocess.check_call("ls -l", shell=True)
subprocess.check_output("ls -l", shell=True)
subprocess.check_output("ls -l", shell=True)
```
- Without using the `subprocess` module, we can use the `os` module to execute bash commands in Python.
```python
import os

os.system("ls -l")
os.popen("ls -l")
os.popen("ls -l").read()
```

### readline(s), hasline(s) and writeline(s) methods
- The `readline()` method reads a single line from a file.
- The `readlines()` method reads all the lines from a file.
- The `hasline()` method checks if a file has a line.
- The `writeline()` method writes a single line to a file.
- The `writelines()` method writes multiple lines to a file.

```python
with open("file.txt", "r") as file:
    line = file.readline()
    lines = file.readlines()
    has_line = file.hasline()
    file.writeline("Hello")
    file.writelines(["Hello", "World"])
```

### learning os module in Python
- The `os` module provides a way to interact with the operating system.
```python
import os

print(os.getcwd())
print(os.listdir())
os.mkdir("test")
os.rmdir("test")
os.remove("file.txt")
os.rename("file.txt", "new.txt")
os.path.exists("file.txt")
os.path.isfile("file.txt")
os.path.isdir("file.txt")
```