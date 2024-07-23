---
layout: post
title:  "Advance Python Tutorials"
date:   2019-02-05 00:04:58 +0530
categories: general
summary: Contains advance python tutorials.
---

### 1. Decorators

**Function Decorators**:
```python
def my_decorator(func):
    def wrapper():
        print("Something is happening before the function is called.")
        func()
        print("Something is happening after the function is called.")
    return wrapper

@my_decorator
def say_hello():
    print("Hello!")

say_hello()
```

**Class Decorators**:
```python
def decorator(cls):
    class WrappedClass:
        def __init__(self, *args, **kwargs):
            self.wrapped = cls(*args, **kwargs)
        def __getattr__(self, name):
            return getattr(self.wrapped, name)
        def new_method(self):
            print("New method added by decorator")
    return WrappedClass

@decorator
class MyClass:
    def method(self):
        print("Original method")

obj = MyClass()
obj.method()
obj.new_method()
```

### 2. Context Managers

**Using the `with` statement**:
```python
with open('file.txt', 'w') as f:
    f.write('Hello, world!')
```

**Custom Context Managers**:
```python
class MyContextManager:
    def __enter__(self):
        print("Entering the context")
        return self
    def __exit__(self, exc_type, exc_value, traceback):
        print("Exiting the context")

with MyContextManager():
    print("Inside the context")
```

### 3. Generators and Iterators

**Creating and Using Generators**:
```python
def my_generator():
    yield 1
    yield 2
    yield 3

for value in my_generator():
    print(value)
```

**Custom iterators using __iter__ and __next__ methods**:
```python
class MyIterator:
    def __init__(self, start, end):
        self.current = start
        self.end = end
    def __iter__(self):
        return self
    def __next__(self):
        if self.current > self.end:
            raise StopIteration
        else:
            self.current += 1
            return self.current - 1

for num in MyIterator(1, 5):
    print(num)
```

### 4. Metaclasses

```python
class MyMeta(type):
    def __new__(cls, name, bases, dct):
        print(f"Creating class {name}")
        return super().__new__(cls, name, bases, dct)

class MyClass(metaclass=MyMeta):
    pass
```

### 5. Descriptors

```python
class MyDescriptor:
    def __get__(self, instance, owner):
        return 'Value from descriptor'
    def __set__(self, instance, value):
        print('Setting value:', value)

class MyClass:
    attr = MyDescriptor()

obj = MyClass()
print(obj.attr)
obj.attr = 'New Value'
```

### 6. Coroutines and Asyncio

```python
import asyncio

async def say_hello():
    print('Hello')
    await asyncio.sleep(1)
    print('World')

asyncio.run(say_hello())
```

### 7. Type Hints and Annotations

```python
def greet(name: str) -> str:
    return f"Hello, {name}"

print(greet("Alice"))
```

### 8. Contextual Attributes

```python
import threading

local_data = threading.local()
local_data.value = 42

def worker():
    local_data.value = 100
    print(f"Worker thread value: {local_data.value}")

thread = threading.Thread(target=worker)
thread.start()
thread.join()

print(f"Main thread value: {local_data.value}")
```

### 9. Advanced OOP Concepts

**Mixins**:
```python
class Mixin:
    def mixin_method(self):
        print("Mixin method")

class MyClass(Mixin):
    def my_method(self):
        print("MyClass method")

obj = MyClass()
obj.my_method()
obj.mixin_method()
```

### 10. Functional Programming

```python
from functools import reduce

numbers = [1, 2, 3, 4, 5]

# Map
squared = map(lambda x: x**2, numbers)
print(list(squared))

# Filter
evens = filter(lambda x: x % 2 == 0, numbers)
print(list(evens))

# Reduce
summed = reduce(lambda x, y: x + y, numbers)
print(summed)
```

### 11. Memory Management

```python
import weakref

class MyClass:
    pass

obj = MyClass()
r = weakref.ref(obj)

print(r())  # Output: <__main__.MyClass object at 0x...>
del obj
print(r())  # Output: None
```

### 12. Cython and Performance Optimization

**Using Cython**:
Save the following code in a file named `example.pyx`:
```python
def say_hello_to(name):
    print(f"Hello {name}!")
```

Then, compile and use it in Python:
```sh
cythonize -i example.pyx
```

```python
import example
example.say_hello_to("World")
```

### 13. Concurrency

**Threading**:
```python
import threading

def worker():
    print("Worker thread")

thread = threading.Thread(target=worker)
thread.start()
thread.join()
```

**Multiprocessing**:
```python
from multiprocessing import Process

def worker():
    print("Worker process")

process = Process(target=worker)
process.start()
process.join()
```

### 14. Networking

**Sockets**:
```python
import socket

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('example.com', 80))
s.sendall(b'GET / HTTP/1.1\r\nHost: example.com\r\n\r\n')
response = s.recv(1024)
print(response)
s.close()
```

**High-level Networking**:
```python
import requests

response = requests.get('https://api.github.com')
print(response.json())
```

### 15. Meta-programming

**Code Generation**:
```python
code = """
def generated_function():
    return 'Hello from generated function'
"""

exec(code)
print(generated_function())
```

### 16. Data Classes and Named Tuples

**Data Classes**:
```python
from dataclasses import dataclass

@dataclass
class Point:
    x: int
    y: int

p = Point(1, 2)
print(p)
```

**Named Tuples**:
```python
from collections import namedtuple

Point = namedtuple('Point', ['x', 'y'])
p = Point(1, 2)
print(p)
```

### 17. Decorating Classes

**Class and Static Methods**:
```python
class MyClass:
    @classmethod
    def class_method(cls):
        print("Class method")
    
    @staticmethod
    def static_method():
        print("Static method")

MyClass.class_method()
MyClass.static_method()
```

**Property Decorators**:
```python
class MyClass:
    def __init__(self, value):
        self._value = value

    @property
    def value(self):
        return self._value

    @value.setter
    def value(self, new_value):
        self._value = new_value

obj = MyClass(10)
print(obj.value)
obj.value = 20
print(obj.value)
```

### 18. Working with C Extensions

**Using `ctypes`**:
```python
import ctypes

libc = ctypes.CDLL("libc.so.6")
libc.printf(b"Hello, World!\n")
```

### 19. Security

**Avoiding Injection Attacks**:
```python
import sqlite3

conn = sqlite3.connect(':memory:')
c = conn.cursor()
c.execute("CREATE TABLE users (id INTEGER, name TEXT)")

# Unsafe way (vulnerable to SQL injection)
unsafe_name = "Alice'; DROP TABLE users; --"
c.execute(f"INSERT INTO users (name) VALUES ('{unsafe_name}')")

# Safe way
safe_name = "Alice"
c.execute("INSERT INTO users (name) VALUES (?)", (safe_name,))
```

### 20. Testing and Debugging

**Using `unittest`**:
```python
import unittest

class TestStringMethods(unittest.TestCase):
    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

if __name__ == '__main__':
    unittest.main()
```

**Using `pdb`**:
```python
import pdb

def my_function():
    pdb.set_trace()
    print("Hello, World!")

my_function()
