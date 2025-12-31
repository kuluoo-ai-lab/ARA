# PYTHON LANGUAGE FORMAL SPECIFICATION
## 12 PRIMARY PYTHON KEYWORDS

### 1. **IMPORT** - Module & Library Management
```python
# Standard imports
import os
import sys
from datetime import datetime
from pathlib import Path

# Specific imports
from typing import List, Dict, Optional, Tuple, Union
from dataclasses import dataclass
from enum import Enum

# Conditional imports
try:
    import numpy as np
except ImportError:
    np = None

# Relative imports
from .module import function
from ..parent import Class

# Rules: Use absolute imports, prefer explicit imports, organize by standard/third-party/local
```

### 2. **VARIABLE** - Variable Declaration & Typing
```python
# Basic assignment
name = "John"
age = 30
is_active = True

# Type hints
message: str = "Hello"
count: int = 0
items: List[str] = []
mapping: Dict[str, int] = {}
optional_value: Optional[str] = None

# Constants
MAX_RETRIES = 3
DEFAULT_TIMEOUT = 5.0
BASE_URL = "https://api.example.com"

# Naming conventions
snake_case_variable = "correct"
CONSTANT_VALUE = "uppercase"
_private_variable = "internal"
__dunder_variable = "name mangling"

# Rules: Always use type hints, use snake_case, constants UPPER_CASE
```

### 3. **DATATYPE** - Built-in Data Types
```python
# Primitives
string: str = "text"
integer: int = 42
floating: float = 3.14
boolean: bool = True
none_type: None = None

# Collections
list_items: List[int] = [1, 2, 3]
tuple_items: Tuple[int, str] = (1, "text")
dict_items: Dict[str, int] = {"a": 1, "b": 2}
set_items: set[int] = {1, 2, 3}

# Dataclass
@dataclass
class Person:
    name: str
    age: int
    email: Optional[str] = None

# Named tuple
from typing import NamedTuple
class Point(NamedTuple):
    x: float
    y: float

# Rules: Prefer dataclasses over plain classes, use type hints
```

### 4. **FUNCTION** - Function Definition & Invocation
```python
# Basic function
def add(a: int, b: int) -> int:
    """Add two numbers."""
    return a + b

# Default parameters
def greet(name: str = "Guest") -> str:
    return f"Hello, {name}"

# Variable arguments
def sum_all(*args: int) -> int:
    return sum(args)

# Keyword arguments
def config(**kwargs: str) -> Dict[str, str]:
    return kwargs

# Type hints with complex types
def process(
    items: List[str],
    callback: Callable[[str], bool]
) -> Dict[str, int]:
    """Process items with callback."""
    return {}

# Async functions
async def fetch_data(url: str) -> dict:
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.json()

# Rules: Always add docstrings, use type hints, single responsibility
```

### 5. **CLASS** - Object-Oriented Programming
```python
# Basic class
class Animal:
    def __init__(self, name: str) -> None:
        self.name = name
    
    def speak(self) -> str:
        return f"{self.name} speaks"

# Inheritance
class Dog(Animal):
    def speak(self) -> str:
        return f"{self.name} barks"

# Dataclass
@dataclass
class Person:
    name: str
    age: int
    
    def is_adult(self) -> bool:
        return self.age >= 18

# Abstract base class
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self) -> float:
        pass

class Circle(Shape):
    def __init__(self, radius: float) -> None:
        self.radius = radius
    
    def area(self) -> float:
        return 3.14159 * self.radius ** 2

# Rules: Use dataclasses for simple data, inheritance for behavior
```

### 6. **CONTROL** - Control Flow Structures
```python
# If/elif/else
if age >= 18:
    status = "adult"
elif age >= 13:
    status = "teenager"
else:
    status = "child"

# Ternary
status = "adult" if age >= 18 else "minor"

# Switch (Python 3.10+)
match status:
    case "adult":
        print("18+")
    case "teenager":
        print("13-17")
    case _:
        print("child")

# Try/except
try:
    result = int("invalid")
except ValueError as e:
    print(f"Error: {e}")
except Exception as e:
    print(f"Unexpected: {e}")
finally:
    cleanup()

# Rules: Use specific exceptions, always have except clauses
```

### 7. **LOOP** - Iteration Structures
```python
# For loop with enumerate
for index, item in enumerate(items):
    print(f"{index}: {item}")

# For loop with zip
for name, age in zip(names, ages):
    print(f"{name} is {age}")

# While loop
count = 0
while count < 10:
    print(count)
    count += 1

# List comprehension (preferred)
squared = [x ** 2 for x in range(10)]
evens = [x for x in range(10) if x % 2 == 0]

# Dictionary comprehension
mapping = {x: x ** 2 for x in range(5)}

# Generator expression
total = sum(x ** 2 for x in range(1000))

# Rules: Prefer comprehensions over loops, use enumerate/zip
```

### 8. **STRING** - String Operations & Formatting
```python
# F-strings (preferred)
name = "World"
greeting = f"Hello, {name}!"

# Format method
message = "Hello, {}!".format(name)
formatted = "Name: {name}, Age: {age}".format(name=name, age=age)

# String methods
text = "  Hello World  "
text.strip()              # Remove whitespace
text.lower()              # Convert to lowercase
text.split()              # Split into list
" ".join(words)           # Join list to string
text.replace("o", "0")    # Replace substring

# String checking
text.startswith("Hello")
text.endswith("World")
"lo" in text

# Multiline strings
docstring = """
This is a
multiline string
"""

# Rules: Use f-strings, leverage string methods
```

### 9. **ERROR** - Error Handling & Validation
```python
# Custom exceptions
class ValidationError(Exception):
    """Raised when validation fails."""
    pass

class NotFoundError(Exception):
    """Raised when item not found."""
    pass

# Raising exceptions
if not email:
    raise ValidationError("Email required")

# Context managers
from contextlib import contextmanager

@contextmanager
def database_connection():
    connection = db.connect()
    try:
        yield connection
    finally:
        connection.close()

# Using context managers
with database_connection() as conn:
    conn.query("SELECT * FROM users")

# Rules: Create custom exceptions, use context managers
```

### 10. **DECORATOR** - Function & Class Decorators
```python
# Function decorator
def timer(func):
    def wrapper(*args, **kwargs):
        import time
        start = time.time()
        result = func(*args, **kwargs)
        duration = time.time() - start
        print(f"Took {duration:.2f}s")
        return result
    return wrapper

@timer
def slow_function():
    import time
    time.sleep(2)

# Class decorator
def add_repr(cls):
    def __repr__(self):
        attrs = ", ".join(f"{k}={v}" for k, v in self.__dict__.items())
        return f"{cls.__name__}({attrs})"
    cls.__repr__ = __repr__
    return cls

@add_repr
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Built-in decorators
@property
def age(self) -> int:
    return self._age

@staticmethod
def from_dict(data: dict) -> "Person":
    return Person(**data)

# Rules: Use decorators for cross-cutting concerns
```

### 11. **ASYNC** - Asynchronous Programming
```python
import asyncio
import aiohttp

# Async function
async def fetch_url(url: str) -> str:
    async with aiohttp.ClientSession() as session:
        async with session.get(url) as response:
            return await response.text()

# Async context manager
class AsyncDatabase:
    async def __aenter__(self):
        await self.connect()
        return self
    
    async def __aexit__(self, exc_type, exc_val, exc_tb):
        await self.disconnect()

# Using async context manager
async with AsyncDatabase() as db:
    await db.query("SELECT * FROM users")

# Running async code
async def main():
    results = await asyncio.gather(
        fetch_url("https://example.com"),
        fetch_url("https://google.com")
    )
    return results

if __name__ == "__main__":
    asyncio.run(main())

# Rules: Use async/await, leverage asyncio for concurrency
```

### 12. **TESTING** - Unit Testing & Quality
```python
import pytest
from unittest import TestCase

# Pytest style
def test_add():
    assert add(2, 3) == 5
    assert add(0, 0) == 0
    assert add(-1, 1) == 0

def test_add_with_floats():
    assert abs(add(2.5, 3.5) - 6.0) < 0.001

@pytest.mark.parametrize("a,b,expected", [
    (2, 3, 5),
    (0, 0, 0),
    (-1, 1, 0),
])
def test_add_parametrized(a, b, expected):
    assert add(a, b) == expected

# Unittest style
class TestCalculator(TestCase):
    def test_add(self):
        self.assertEqual(add(2, 3), 5)
    
    def setUp(self):
        self.calc = Calculator()
    
    def tearDown(self):
        self.calc.reset()

# Fixtures
@pytest.fixture
def sample_data():
    return {"users": [{"id": 1, "name": "John"}]}

def test_with_fixture(sample_data):
    assert len(sample_data["users"]) == 1

# Rules: Test behavior, aim for 80%+ coverage, use fixtures
```

## 6-STEP PYTHON GENERATION WORKFLOW

### STEP-1: UNDERSTAND INTENT
- Package/module purpose?
- Dependencies needed?
- Python version (3.9+)?
- Async requirements?
- Testing framework?

### STEP-2: PROJECT STRUCTURE
```
myproject/
├── src/
│   ├── __init__.py
│   └── module.py
├── tests/
│   ├── __init__.py
│   └── test_module.py
├── docs/
├── requirements.txt
├── pyproject.toml
└── README.md
```

### STEP-3: RETRIEVE PYTHON RULES
```
Rules:
- Type hints everywhere
- Snake_case for variables/functions
- PEP 8 compliance
- Docstrings for all functions
- Context managers for resources
- Async for I/O operations
- Custom exceptions
- Comprehensive testing
```

### STEP-4: REQUIREMENTS CHECKLIST
```
☐ Type hints added
☐ Docstrings complete
☐ Error handling present
☐ Tests written (80%+)
☐ PEP 8 compliant
☐ Requirements documented
☐ README complete
☐ Configuration in pyproject.toml
```

### STEP-5: GENERATION ROADMAP
```
PHASE 1: PROJECT SETUP
├─ Package structure
├─ requirements.txt
└─ pyproject.toml

PHASE 2: CORE MODULES
├─ Data models
├─ Utilities
└─ Core logic

PHASE 3: ERROR HANDLING
├─ Custom exceptions
├─ Validation
└─ Logging

PHASE 4: API LAYER
├─ Async functions
├─ Database interface
└─ External API calls

PHASE 5: TESTING
├─ Unit tests
├─ Integration tests
└─ Edge cases

PHASE 6: DOCUMENTATION
├─ Docstrings
├─ Type hints
├─ README
└─ Examples
```

### STEP-6: EXECUTE GENERATION
```python
#!/usr/bin/env python3
"""Module docstring."""

from typing import List, Optional, Dict
from dataclasses import dataclass
from abc import ABC, abstractmethod
import logging
import asyncio

# Logging setup
logger = logging.getLogger(__name__)

# Data models
@dataclass
class User:
    """User data model."""
    id: int
    name: str
    email: str

# Abstract base
class Repository(ABC):
    """Base repository interface."""
    
    @abstractmethod
    async def get(self, id: int) -> Optional[User]:
        """Get user by ID."""
        pass

# Implementation
class UserRepository(Repository):
    """User repository implementation."""
    
    def __init__(self) -> None:
        """Initialize repository."""
        self.users: Dict[int, User] = {}
    
    async def get(self, id: int) -> Optional[User]:
        """Get user by ID."""
        return self.users.get(id)
    
    async def create(self, user: User) -> User:
        """Create new user."""
        self.users[user.id] = user
        logger.info(f"Created user: {user.name}")
        return user

# Error handling
class UserNotFoundError(Exception):
    """Raised when user not found."""
    pass

# Service layer
class UserService:
    """User service."""
    
    def __init__(self, repo: Repository) -> None:
        """Initialize service."""
        self.repo = repo
    
    async def get_user(self, id: int) -> User:
        """Get user by ID."""
        user = await self.repo.get(id)
        if not user:
            raise UserNotFoundError(f"User {id} not found")
        return user

# Testing
if __name__ == "__main__":
    import pytest
    pytest.main([__file__])
```

## BEST PRACTICES

1. **Always use type hints** - For functions and variables
2. **Follow PEP 8** - Use linters (pylint, flake8)
3. **Docstrings for all** - Functions, classes, modules
4. **Use dataclasses** - For simple data models
5. **Handle exceptions** - Specific exceptions, never bare except
6. **Async for I/O** - Use asyncio for concurrent operations
7. **Test thoroughly** - Unit and integration tests
8. **Log properly** - Use logging module, not print()
9. **DRY principle** - Don't repeat yourself
10. **Use virtual environments** - Keep dependencies isolated

---
