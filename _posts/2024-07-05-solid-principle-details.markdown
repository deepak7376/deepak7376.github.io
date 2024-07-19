---
layout: post
title:  "SOLID Principles with Code Examples"
date:   2024-07-05 00:04:58 +0530
categories: general
summary: SOLID Principles with Code Examples.
---
---

## SOLID Principles with Code Examples

### 1. Single Responsibility Principle (SRP)

**Definition:** A class should have only one reason to change.

**Example:**

```python
class User:
    def __init__(self, username, email):
        self.username = username
        self.email = email

    def get_username(self):
        return self.username

    def get_email(self):
        return self.email

class UserManager:
    def __init__(self):
        self.users = []

    def add_user(self, user):
        self.users.append(user)

    def remove_user(self, user):
        self.users.remove(user)

    def send_email_to_all_users(self, message):
        for user in self.users:
            print(f"Sending email to {user.get_email()}: {message}")

# Example usage:
user1 = User("Alice", "alice@example.com")
user2 = User("Bob", "bob@example.com")

manager = UserManager()
manager.add_user(user1)
manager.add_user(user2)

manager.send_email_to_all_users("Welcome to our platform!")
```

In this example, `User` class handles user data, while `UserManager` class manages operations related to users, including adding/removing users and sending emails. Each class has a single responsibility: managing user data and managing user operations.

### 2. Open/Closed Principle (OCP)

**Definition:** Classes should be open for extension but closed for modification.

**Example:**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height
    
    def area(self):
        return self.width * self.height

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return 3.14 * self.radius * self.radius

# Example usage:
rect = Rectangle(5, 10)
print(f"Area of rectangle: {rect.area()}")

circle = Circle(5)
print(f"Area of circle: {circle.area()}")
```

In this example, `Shape` is an abstract base class defining an interface for calculating area. `Rectangle` and `Circle` are concrete implementations of `Shape`, extending it to calculate area based on their specific shapes. This design allows adding new shapes (extension) without modifying existing code (closed for modification).

### 3. Liskov Substitution Principle (LSP)

**Definition:** Subtypes should be substitutable for their base types without affecting the correctness of the program.

**Example:**

```python
class Bird:
    def fly(self):
        pass

class Duck(Bird):
    def fly(self):
        print("Duck flying")

class Ostrich(Bird):
    def fly(self):
        raise NotImplementedError("Ostrich cannot fly")

# Example usage:
def make_bird_fly(bird):
    bird.fly()

duck = Duck()
ostrich = Ostrich()

make_bird_fly(duck)    # Output: Duck flying
make_bird_fly(ostrich) # Raises NotImplementedError
```

In this example, `Duck` and `Ostrich` are subclasses of `Bird`. While `Duck` implements `fly` method, `Ostrich` raises an error for `fly`, adhering to LSP where `Duck` and `Ostrich` can substitute `Bird` but `Ostrich` doesn't perform flying.

### 4. Interface Segregation Principle (ISP)

**Definition:** Clients should not be forced to depend on interfaces they do not use.

**Example:**

```python
from abc import ABC, abstractmethod

# Bad example violating ISP
class Worker(ABC):
    @abstractmethod
    def work(self):
        pass

    @abstractmethod
    def eat(self):
        pass

class Engineer(Worker):
    def work(self):
        print("Engineering work")

    def eat(self):
        print("Engineering lunch break")

class Cleaner(Worker):
    def work(self):
        print("Cleaning work")

    def eat(self):
        print("Cleaning lunch break")

# Better approach respecting ISP
class Workable(ABC):
    @abstractmethod
    def work(self):
        pass

class Eatable(ABC):
    @abstractmethod
    def eat(self):
        pass

class Engineer(Workable, Eatable):
    def work(self):
        print("Engineering work")

    def eat(self):
        print("Engineering lunch break")

class Cleaner(Workable, Eatable):
    def work(self):
        print("Cleaning work")

    def eat(self):
        print("Cleaning lunch break")
```

In the bad example, `Worker` interface forces both `Engineer` and `Cleaner` to implement methods they may not need (`eat`). The better approach introduces separate interfaces (`Workable` and `Eatable`), allowing classes to implement only what they need, adhering to ISP.

### 5. Dependency Inversion Principle (DIP)

**Definition:** Depend on abstractions, not on concretions.

**Example:**

```python
class Switch:
    def __init__(self, device):
        self.device = device

    def turn_on(self):
        self.device.turn_on()

    def turn_off(self):
        self.device.turn_off()

class Light:
    def turn_on(self):
        print("Light is on")

    def turn_off(self):
        print("Light is off")

class Fan:
    def turn_on(self):
        print("Fan is on")

    def turn_off(self):
        print("Fan is off")

# Example usage:
light = Light()
switch = Switch(light)
switch.turn_on()  # Output: Light is on

fan = Fan()
switch = Switch(fan)
switch.turn_on()   # Output: Fan is on
```

In this example, `Switch` depends on `device` abstraction (`turn_on` and `turn_off` methods) rather than specific implementations (`Light` or `Fan`). This allows switching between different devices (`Light` or `Fan`) without modifying `Switch`, adhering to DIP.

---
