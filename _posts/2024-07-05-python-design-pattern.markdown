---
layout: post
comments: true
title:  "Python Design Patterns"
date:   2024-07-05 00:04:58 +0530
categories: general
description: Python Design Patterns.
---
---

## Python Design Patterns

### 1. Singleton Pattern
**Definition**: Ensures a class has only one instance and provides a global point of access to it.

**Example**:

```python
class Singleton:
    _instance = None

    def __new__(cls, *args, **kwargs):
        if not cls._instance:
            cls._instance = super(Singleton, cls).__new__(cls, *args, **kwargs)
        return cls._instance

# Testing the Singleton pattern
singleton1 = Singleton()
singleton2 = Singleton()
print(singleton1 is singleton2)  # Output: True
```

### 2. Factory Pattern
**Definition**: Defines an interface for creating an object, but let subclasses alter the type of objects that will be created.

**Example**:

```python
class Shape:
    def draw(self):
        raise NotImplementedError

class Circle(Shape):
    def draw(self):
        print("Drawing a Circle")

class Square(Shape):
    def draw(self):
        print("Drawing a Square")

class ShapeFactory:
    @staticmethod
    def create_shape(shape_type):
        if shape_type == "Circle":
            return Circle()
        elif shape_type == "Square":
            return Square()
        else:
            return None

# Testing the Factory pattern
factory = ShapeFactory()
shape1 = factory.create_shape("Circle")
shape1.draw()  # Output: Drawing a Circle
shape2 = factory.create_shape("Square")
shape2.draw()  # Output: Drawing a Square
```

### 3. Observer Pattern
**Definition**: Defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

**Example**:

```python
class Subject:
    def __init__(self):
        self._observers = []

    def attach(self, observer):
        if observer not in self._observers:
            self._observers.append(observer)

    def detach(self, observer):
        try:
            self._observers.remove(observer)
        except ValueError:
            pass

    def notify(self, modifier=None):
        for observer in self._observers:
            if modifier != observer:
                observer.update(self)

class Data(Subject):
    def __init__(self, name=''):
        Subject.__init__(self)
        self._name = name
        self._data = 0

    @property
    def data(self):
        return self._data

    @data.setter
    def data(self, value):
        self._data = value
        self.notify()

class HexViewer:
    def update(self, subject):
        print(f'HexViewer: Subject {subject._name} has data 0x{subject.data:x}')

class DecimalViewer:
    def update(self, subject):
        print(f'DecimalViewer: Subject {subject._name} has data {subject.data}')

# Testing the Observer pattern
data = Data('test')
view1 = DecimalViewer()
view2 = HexViewer()

data.attach(view1)
data.attach(view2)

data.data = 10
data.data = 15
```

### 4. Strategy Pattern
**Definition**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. Strategy lets the algorithm vary independently from clients that use it.

**Example**:

```python
class Strategy:
    def do_operation(self, num1, num2):
        raise NotImplementedError

class OperationAdd(Strategy):
    def do_operation(self, num1, num2):
        return num1 + num2

class OperationSubtract(Strategy):
    def do_operation(self, num1, num2):
        return num1 - num2

class OperationMultiply(Strategy):
    def do_operation(self, num1, num2):
        return num1 * num2

class Context:
    def __init__(self, strategy):
        self._strategy = strategy

    def execute_strategy(self, num1, num2):
        return self._strategy.do_operation(num1, num2)

# Testing the Strategy pattern
context = Context(OperationAdd())
print(context.execute_strategy(10, 5))  # Output: 15

context = Context(OperationSubtract())
print(context.execute_strategy(10, 5))  # Output: 5

context = Context(OperationMultiply())
print(context.execute_strategy(10, 5))  # Output: 50
```

### 5. Decorator Pattern
**Definition**: Allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class.

**Example**:

```python
def make_bold(func):
    def wrapped():
        return f"<b>{func()}</b>"
    return wrapped

def make_italic(func):
    def wrapped():
        return f"<i>{func()}</i>"
    return wrapped

@make_bold
@make_italic
def hello():
    return "Hello, World!"

# Testing the Decorator pattern
print(hello())  # Output: <b><i>Hello, World!</i></b>
```

### 6. Adapter Pattern
**Definition**: Allows the interface of an existing class to be used as another interface. It is often used to make existing classes work with others without modifying their source code.

**Example**:

```python
class EuropeanSocket:
    def voltage(self):
        return 230

    def live(self):
        return 1

    def neutral(self):
        return -1

    def earth(self):
        return 0

class USASocket:
    def voltage(self):
        return 120

    def live(self):
        return 1

    def neutral(self):
        return 0

class Adapter(USASocket):
    def __init__(self, socket):
        self.socket = socket

    def voltage(self):
        return self.socket.voltage()

    def live(self):
        return self.socket.live()

    def neutral(self):
        return self.socket.neutral()

    def earth(self):
        return self.socket.earth()

# Testing the Adapter pattern
euro_socket = EuropeanSocket()
adapter = Adapter(euro_socket)
print(adapter.voltage())  # Output: 230
```

### 7. Command Pattern
**Definition**: Encapsulates a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

**Example**:

```python
class Command:
    def execute(self):
        raise NotImplementedError

class Light:
    def on(self):
        print("Light is ON")

    def off(self):
        print("Light is OFF")

class LightOnCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.on()

class LightOffCommand(Command):
    def __init__(self, light):
        self.light = light

    def execute(self):
        self.light.off()

class RemoteControl:
    def __init__(self):
        self._commands = {}

    def set_command(self, button, command):
        self._commands[button] = command

    def press_button(self, button):
        if button in self._commands:
            self._commands[button].execute()

# Testing the Command pattern
light = Light()
remote = RemoteControl()
remote.set_command("ON", LightOnCommand(light))
remote.set_command("OFF", LightOffCommand(light))

remote.press_button("ON")  # Output: Light is ON
remote.press_button("OFF")  # Output: Light is OFF
```

### 8. State Pattern
**Definition**: Allows an object to alter its behavior when its internal state changes. The object will appear to change its class.

**Example**:

```python
class State:
    def do_action(self, context):
        raise NotImplementedError

class StartState(State):
    def do_action(self, context):
        print("Player is in start state")
        context.set_state(self)

    def __str__(self):
        return "Start State"

class StopState(State):
    def do_action(self, context):
        print("Player is in stop state")
        context.set_state(self)

    def __str__(self):
        return "Stop State"

class Context:
    def __init__(self):
        self._state = None

    def set_state(self, state):
        self._state = state

    def get_state(self):
        return self._state

# Testing the State pattern
context = Context()

start_state = StartState()
start_state.do_action(context)
print(context.get_state())  # Output: Start State

stop_state = StopState()
stop_state.do_action(context)
print(context.get_state())  # Output: Stop State
```

### 9. Template Method Pattern
**Definition**: Defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Template Method lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

**Example**:

```python
from abc import ABC, abstractmethod

class Game(ABC):
    def play(self):
        self.initialize()
        self.start_play()
        self.end_play()

    @abstractmethod
    def initialize(self):
        pass

    @abstractmethod
    def start_play(self):
        pass

    @abstractmethod
    def end_play(self):
        pass

class Cricket(Game):
    def initialize(self):
        print("Cricket Game Initialized! Start playing.")

    def start_play(self):
        print("Cricket Game Started. Enjoy the game!")

    def end_play(self):
        print("Cricket Game Finished!")

class Football(Game):
    def initialize(self):
        print("Football Game Initialized! Start playing.")

    def start_play(self):
        print("Football Game Started. Enjoy the game!")

    def end_play(self):
        print("Football Game Finished!")

# Testing the Template Method pattern
cricket = Cricket()
cricket.play()
# Output:
# Cricket Game Initialized! Start playing.
# Cricket Game Started. Enjoy the game!
# Cricket Game Finished!

football = Football()
football.play()
# Output:
# Football Game Initialized! Start playing.
# Football Game Started. Enjoy the game!
# Football Game Finished!
```

### 10. Builder Pattern
**Definition**: Separates the construction of a complex object from its representation so that the same construction process can create different representations.

**Example**:

```python
class Burger:
    def __init__(self):
        self._ingredients = []

    def add_ingredient(self, ingredient):
        self._ingredients.append(ingredient)

    def show(self):
        print(f'Burger with: {", ".join(self._ingredients)}')

class BurgerBuilder:
    def __init__(self):
        self.burger = Burger()

    def add_lettuce(self):
        self.burger.add_ingredient('lettuce')
        return self

    def add_tomato(self):
        self.burger.add_ingredient('tomato')
        return self

    def add_patty(self):
        self.burger.add_ingredient('patty')
        return self

    def build(self):
        return self.burger

# Testing the Builder pattern
builder = BurgerBuilder()
burger = builder.add_lettuce().add_tomato().add_patty().build()
burger.show()  # Output: Burger with: lettuce, tomato, patty
```

### 11. Prototype Pattern
**Definition**: Specifies the kinds of objects to create using a prototypical instance, and create new objects by copying this prototype.

**Example**:

```python
import copy

class Prototype:
    def clone(self):
        return copy.deepcopy(self)

class ConcretePrototype1(Prototype):
    def __init__(self, value):
        self.value = value

# Testing the Prototype pattern
prototype = ConcretePrototype1(42)
clone = prototype.clone()
print(prototype.value)  # Output: 42
print(clone.value)  # Output: 42
print(prototype is clone)  # Output: False
```

### 12. Chain of Responsibility Pattern
**Definition**: Allows an object to send a command without knowing what object will receive and handle it. Each object in the chain passes the command along the chain until an object handles it.

**Example**:

```python
class Handler:
    def __init__(self, successor=None):
        self._successor = successor

    def handle(self, request):
        handled = self._handle(request)
        if not handled:
            self._successor.handle(request)

    def _handle(self, request):
        raise NotImplementedError

class ConcreteHandler1(Handler):
    def _handle(self, request):
        if 0 < request <= 10:
            print(f"Request {request} handled by handler 1")
            return True

class ConcreteHandler2(Handler):
    def _handle(self, request):
        if 10 < request <= 20:
            print(f"Request {request} handled by handler 2")
            return True

class DefaultHandler(Handler):
    def _handle(self, request):
        print(f"Request {request} handled by default handler")
        return True

# Testing the Chain of Responsibility pattern
h1 = ConcreteHandler1()
h2 = ConcreteHandler2(h1)
default_handler = DefaultHandler(h2)

default_handler.handle(5)   # Output: Request 5 handled by handler 1
default_handler.handle(15)  # Output: Request 15 handled by handler 2
default_handler.handle(25)  # Output: Request 25 handled by default handler
```

### 13. Mediator Pattern
**Definition**: Defines an object that encapsulates how a set of objects interact. This pattern promotes loose coupling by keeping objects from referring to each other explicitly.

**Example**:

```python
class Mediator:
    def notify(self, sender, event):
        raise NotImplementedError

class ConcreteMediator(Mediator):
    def __init__(self):
        self._component1 = None
        self._component2 = None

    def set_components(self, component1, component2):
        self._component1 = component1
        self._component2 = component2

    def notify(self, sender, event):
        if event == "A":
            print("Mediator reacts on A and triggers the following operations:")
            self._component2.do_c()
        elif event == "D":
            print("Mediator reacts on D and triggers the following operations:")
            self._component1.do_b()
            self._component2.do_c()

class BaseComponent:
    def __init__(self, mediator=None):
        self._mediator = mediator

    def set_mediator(self, mediator):
        self._mediator = mediator

class Component1(BaseComponent):
    def do_a(self):
        print("Component 1 does A.")
        self._mediator.notify(self, "A")

    def do_b(self):
        print("Component 1 does B.")

class Component2(BaseComponent):
    def do_c(self):
        print("Component 2 does C.")

    def do_d(self):
        print("Component 2 does D.")
        self._mediator.notify(self, "D")

# Testing the Mediator pattern
mediator = ConcreteMediator()
c1 = Component1()
c2 = Component2()
mediator.set_components(c1, c2)

c1.set_mediator(mediator)
c2.set_mediator(mediator)

c1.do_a()
# Output:
# Component 1 does A.
# Mediator reacts on A and triggers the following operations:
# Component 2 does C.

c2.do_d()
# Output:
# Component 2 does D.
# Mediator reacts on D and triggers the following operations:
# Component 1 does B.
# Component 2 does C.
```

### 14. Memento Pattern
**Definition**: Provides the ability to restore an object to its previous state (undo via rollback).

**Example**:

```python
class Memento:
    def __init__(self, state):
        self._state = state

    def get_state(self):
        return self._state

class Originator:
    def __init__(self, state):
        self._state = state

    def set_state(self, state):
        print(f"Setting state to {state}")
        self._state = state

    def save_state_to_memento(self):
        print("Saving state to Memento")
        return Memento(self._state)

    def get_state_from_memento(self, memento):
        self._state = memento.get_state()
        print(f"Restoring state from Memento: {self._state}")

# Testing the Memento pattern
originator = Originator("State1")
memento = originator.save_state_to_memento()
originator.set_state("State2")

originator.get_state_from_memento(memento)
# Output:
# Saving state to Memento
# Setting state to State2
# Restoring state from Memento: State1
```

### 15. Visitor Pattern
**Definition**: Lets you separate algorithms from the objects on which they operate.

**Example**:

```python
class Element:
    def accept(self, visitor):
        raise NotImplementedError

class ConcreteElementA(Element):
    def accept(self, visitor):
        visitor.visit_concrete_element_a(self)

    def operation_a(self):
        return "ConcreteElementA"

class ConcreteElementB(Element):
    def accept(self, visitor):
        visitor.visit_concrete_element_b(self)

    def operation_b(self):
        return "ConcreteElementB"

class Visitor:
    def visit_concrete_element_a(self, element):
        raise NotImplementedError

    def visit_concrete_element_b(self, element):
        raise NotImplementedError

class ConcreteVisitor1(Visitor):
    def visit_concrete_element_a(self, element):
        print(f"{element.operation_a()} visited by ConcreteVisitor1")

    def visit_concrete_element_b(self, element):
        print(f"{element.operation_b()} visited by ConcreteVisitor1")

class ConcreteVisitor2(Visitor):
    def visit_concrete_element_a(self, element):
        print(f"{element.operation_a()} visited by ConcreteVisitor2")

    def visit_concrete_element_b(self, element):
        print(f"{element.operation_b()} visited by ConcreteVisitor2")

# Testing the Visitor pattern
elements = [ConcreteElementA(), ConcreteElementB()]
visitor1 = ConcreteVisitor1()
visitor2 = ConcreteVisitor2()

for element in elements:
    element.accept(visitor1)
    element.accept(visitor2)
# Output:
# ConcreteElementA visited

 by ConcreteVisitor1
# ConcreteElementA visited by ConcreteVisitor2
# ConcreteElementB visited by ConcreteVisitor1
# ConcreteElementB visited by ConcreteVisitor2
