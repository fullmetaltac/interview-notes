# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Creational Design Patterns](#creational-design-patterns)
    - [Factory](#factory)
    - [Abstract Factory](#abstract-factory)
    - [Builder](#builder)
    - [Prototype](#prototype)
    - [Singleton](#singleton)
    - [Object Pool](#object-pool)
    - [Lazy Evaluation](#lazy-evaluation)
  - [Structural Design Patterns](#structural-design-patterns)
    - [Adapter](#adapter)
    - [Bridge](#bridge)
    - [Composite](#composite)
    - [Decorator](#decorator)
    - [Facade](#facade)
    - [Flyweight](#flyweight)
    - [Proxy](#proxy)
  - [Behavioral Design Pattern](#behavioral-design-pattern)
    - [Chain of Responsibility](#chain-of-responsibility)
    - [Command](#command)
    - [Iterator](#iterator)
    - [Mediator](#mediator)
    - [Memento](#memento)
    - [Observer](#observer)
    - [State Method](#state-method)
    - [Strategy](#strategy)
    - [Template](#template)
    - [Visitor](#visitor)
  - [Test Automation](#test-automation)
    - [Page object](#page-object)
  - [References](#references)

## Creational Design Patterns

Creational patterns provides essential information regarding the Class instantiation or the object instantiation. Class Creational Pattern and the Object Creational pattern is the major categorization of the Creational Design Patterns. While class-creation patterns use inheritance effectively in the instantiation process, object-creation patterns use delegation effectively to get the job done.

### Factory 

Creates objects without having to specify the exact class.

```python
from typing import Dict
from typing import Type
from typing import Protocol


class Localizer(Protocol):
    def localize(self, msg: str) -> str:
        pass


class GreekLocalizer:
    def __init__(self) -> None:
        self.translations = {"dog": "σκύλος", "cat": "γάτα"}

    def localize(self, msg: str) -> str:
        return self.translations.get(msg, msg)


class EnglishLocalizer:
    def localize(self, msg: str) -> str:
        return msg


def get_localizer(language: str = "English") -> Localizer:
    localizers: Dict[str, Type[Localizer]] = {
        "English": EnglishLocalizer,
        "Greek": GreekLocalizer,
    }

    return localizers[language]()
```

### Abstract Factory 

Provides a way to encapsulate a group of individual factories.

```python
import random
from typing import Type


class Pet:
    def __init__(self, name: str) -> None:
        self.name = name

    def speak(self) -> None:
        raise NotImplementedError

    def __str__(self) -> str:
        raise NotImplementedError


class Dog(Pet):
    def speak(self) -> None:
        print("woof")

    def __str__(self) -> str:
        return f"Dog<{self.name}>"


class Cat(Pet):
    def speak(self) -> None:
        print("meow")

    def __str__(self) -> str:
        return f"Cat<{self.name}>"


class PetShop:
    def __init__(self, animal_factory: Type[Pet]) -> None:
        self.pet_factory = animal_factory

    def buy_pet(self, name: str) -> Pet:
        pet = self.pet_factory(name)
        print(f"Here is your lovely {pet}")
        return pet


# Additional factories:

def random_animal(name: str) -> Pet:
    """Let's be dynamic!"""
    return random.choice([Dog, Cat])(name)
```

### Builder

Decouples the creation of a complex object and its representation.

```python
class Building:
    def __init__(self) -> None:
        self.build_floor()
        self.build_size()

    def build_floor(self):
        raise NotImplementedError

    def build_size(self):
        raise NotImplementedError

    def __repr__(self) -> str:
        return "Floor: {0.floor} | Size: {0.size}".format(self)


class House(Building):
    def build_floor(self) -> None:
        self.floor = "One"

    def build_size(self) -> None:
        self.size = "Big"


class Flat(Building):
    def build_floor(self) -> None:
        self.floor = "More than One"

    def build_size(self) -> None:
        self.size = "Small"


class ComplexBuilding:
    def __repr__(self) -> str:
        return "Floor: {0.floor} | Size: {0.size}".format(self)


class ComplexHouse(ComplexBuilding):
    def build_floor(self) -> None:
        self.floor = "One"

    def build_size(self) -> None:
        self.size = "Big and fancy"


def construct_building(cls) -> Building:
    building = cls()
    building.build_floor()
    building.build_size()
    return building
```

### Prototype

Creates new object instances by cloning prototype.

```python
from typing import Any
from __future__ import annotations


class Prototype:
    def __init__(self, value: str = "default", **attrs: Any) -> None:
        self.value = value
        self.__dict__.update(attrs)

    def clone(self, **attrs: Any) -> Prototype:
        obj = self.__class__(**self.__dict__)
        obj.__dict__.update(attrs)
        return obj


class PrototypeDispatcher:
    def __init__(self):
        self._objects = {}

    def get_objects(self) -> dict[str, Prototype]:
        return self._objects

    def register_object(self, name: str, obj: Prototype) -> None:
        self._objects[name] = obj

    def unregister_object(self, name: str) -> None:
        del self._objects[name]
```

### Singleton 

Provides singleton-like behavior sharing state between instances.

```python
from typing import Dict


class Borg:
    _shared_state: Dict[str, str] = {}

    def __init__(self) -> None:
        self.__dict__ = self._shared_state


class YourBorg(Borg):
    def __init__(self, state: str = None) -> None:
        super().__init__()
        if state:
            self.state = state
        else:
            if not hasattr(self, "state"):
                self.state = "Init"

    def __str__(self) -> str:
        return self.state
```
### Object Pool

Stores a set of initialized objects kept ready to use.

```python
class ObjectPool:
    def __init__(self, queue, auto_get=False):
        self._queue = queue
        self.item = self._queue.get() if auto_get else None

    def __enter__(self):
        if self.item is None:
            self.item = self._queue.get()
        return self.item

    def __exit__(self, Type, value, traceback):
        if self.item is not None:
            self._queue.put(self.item)
            self.item = None

    def __del__(self):
        if self.item is not None:
            self._queue.put(self.item)
            self.item = None
```


### Lazy Evaluation

Delays the eval of an expr until its value is needed and avoids repeated evals.

```python
import functools


class lazy_property:
    def __init__(self, function):
        self.function = function
        functools.update_wrapper(self, function)

    def __get__(self, obj, type_):
        if obj is None:
            return self
        val = self.function(obj)
        obj.__dict__[self.function.__name__] = val
        return val


def lazy_property2(fn):
    attr = "_lazy__" + fn.__name__

    @property
    def _lazy_property(self):
        if not hasattr(self, attr):
            setattr(self, attr, fn(self))
        return getattr(self, attr)

    return _lazy_property


class Person:
    def __init__(self, name, occupation):
        self.name = name
        self.occupation = occupation
        self.call_count2 = 0

    @lazy_property
    def relatives(self):
        relatives = "Many relatives."
        return relatives

    @lazy_property2
    def parents(self):
        self.call_count2 += 1
        return "Father and mother"
```


## Structural Design Patterns

Structural design patterns are about organizing different classes and objects to form larger structures and provide new functionality while keeping these structures flexible and efficient. Mostly they use Inheritance to compose all the interfaces. It also identifies the relationships which led to the simplification of the structure.

### Adapter

Allows the interface of an existing class to be used as another interface.

```python
from typing import Callable, TypeVar

T = TypeVar("T")


class Dog:
    def __init__(self) -> None:
        self.name = "Dog"

    def bark(self) -> str:
        return "woof!"


class Cat:
    def __init__(self) -> None:
        self.name = "Cat"

    def meow(self) -> str:
        return "meow!"


class Human:
    def __init__(self) -> None:
        self.name = "Human"

    def speak(self) -> str:
        return "'hello'"


class Car:
    def __init__(self) -> None:
        self.name = "Car"

    def make_noise(self, octane_level: int) -> str:
        return f"vroom{'!' * octane_level}"


class Adapter:
    def __init__(self, obj: T, **adapted_methods: Callable):
        self.obj = obj
        self.__dict__.update(adapted_methods)

    def __getattr__(self, attr):
        return getattr(self.obj, attr)

    def original_dict(self):
        return self.obj.__dict__
```

### Bridge

Decouples an abstraction from its implementation.

```python
class DrawingAPI1:
    def draw_circle(self, x, y, radius):
        print(f"API1.circle at {x}:{y} radius {radius}")


class DrawingAPI2:
    def draw_circle(self, x, y, radius):
        print(f"API2.circle at {x}:{y} radius {radius}")


class CircleShape:
    def __init__(self, x, y, radius, drawing_api):
        self._x = x
        self._y = y
        self._radius = radius
        self._drawing_api = drawing_api

    def draw(self):
        self._drawing_api.draw_circle(self._x, self._y, self._radius)

    def scale(self, pct):
        self._radius *= pct
```

### Composite

Describes a group of objects that is treated as a single instance.

```python
from abc import ABC, abstractmethod
from typing import List


class Graphic(ABC):
    @abstractmethod
    def render(self) -> None:
        raise NotImplementedError("You should implement this!")


class CompositeGraphic(Graphic):
    def __init__(self) -> None:
        self.graphics: List[Graphic] = []

    def render(self) -> None:
        for graphic in self.graphics:
            graphic.render()

    def add(self, graphic: Graphic) -> None:
        self.graphics.append(graphic)

    def remove(self, graphic: Graphic) -> None:
        self.graphics.remove(graphic)


class Ellipse(Graphic):
    def __init__(self, name: str) -> None:
        self.name = name

    def render(self) -> None:
        print(f"Ellipse: {self.name}")
```

### Decorator

Adds behaviour to object without affecting its class.

```python
class TextTag:
    def __init__(self, text: str) -> None:
        self._text = text

    def render(self) -> str:
        return self._text


class BoldWrapper(TextTag):
    def __init__(self, wrapped: TextTag) -> None:
        self._wrapped = wrapped

    def render(self) -> str:
        return f"<b>{self._wrapped.render()}</b>"


class ItalicWrapper(TextTag):
    def __init__(self, wrapped: TextTag) -> None:
        self._wrapped = wrapped

    def render(self) -> str:
        return f"<i>{self._wrapped.render()}</i>"
```

### Facade

Provides a simpler unified interface to a complex system.

```python
class CPU:
    def freeze(self) -> None:
        print("Freezing processor.")

    def jump(self, position: str) -> None:
        print("Jumping to:", position)

    def execute(self) -> None:
        print("Executing.")


class Memory:
    def load(self, position: str, data: str) -> None:
        print(f"Loading from {position} data: '{data}'.")


class SolidStateDrive:
    def read(self, lba: str, size: str) -> str:
        return f"Some data from sector {lba} with size {size}"


class ComputerFacade:
    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.ssd = SolidStateDrive()

    def start(self):
        self.cpu.freeze()
        self.memory.load("0x00", self.ssd.read("100", "1024"))
        self.cpu.jump("0x00")
        self.cpu.execute()
```


### Flyweight

Minimizes memory usage by sharing data with other similar objects.

```python
import weakref


class Card:
    _pool: weakref.WeakValueDictionary = weakref.WeakValueDictionary()

    def __new__(cls, value, suit):
        obj = cls._pool.get(value + suit)
        if obj is None:
            obj = object.__new__(Card)
            cls._pool[value + suit] = obj
            obj.value, obj.suit = value, suit
        return obj

    def __repr__(self):
        return f"<Card: {self.value}{self.suit}>"
```

**Flyweight with metaclass**

```python
import weakref

class FlyweightMeta(type):
    def __new__(mcs, name, parents, dct):
        dct["pool"] = weakref.WeakValueDictionary()
        return super().__new__(mcs, name, parents, dct)

    @staticmethod
    def _serialize_params(cls, *args, **kwargs):
        args_list = list(map(str, args))
        args_list.extend([str(kwargs), cls.__name__])
        key = "".join(args_list)
        return key

    def __call__(cls, *args, **kwargs):
        key = FlyweightMeta._serialize_params(cls, *args, **kwargs)
        pool = getattr(cls, "pool", {})

        instance = pool.get(key)
        if instance is None:
            instance = super().__call__(*args, **kwargs)
            pool[key] = instance
        return instance


class Card2(metaclass=FlyweightMeta):
    def __init__(self, *args, **kwargs):
        # print('Init {}: {}'.format(self.__class__, (args, kwargs)))
        pass
```


### Proxy 

Add functionality or logic (e.g. logging, caching, authorization) to a resource
without changing its interface.

```python
from typing import Union


class Subject:
    def do_the_job(self, user: str) -> None:
        raise NotImplementedError()


class RealSubject(Subject):
    def do_the_job(self, user: str) -> None:
        print(f"I am doing the job for {user}")


class Proxy(Subject):
    def __init__(self) -> None:
        self._real_subject = RealSubject()

    def do_the_job(self, user: str) -> None:
        print(f"[log] Doing the job for {user} is requested.")

        if user == "admin":
            self._real_subject.do_the_job(user)
        else:
            print("[log] I can do the job just for `admins`.")


def client(job_doer: Union[RealSubject, Proxy], user: str) -> None:
    job_doer.do_the_job(user)
```


## Behavioral Design Pattern

Behavioral patterns are all about identifying the common communication patterns between objects and realize these patterns. These patterns are concerned with algorithms and the assignment of responsibilities between objects.

### Chain of Responsibility

Allow a request to pass down a chain of receivers until it is handled.

```python
from abc import ABC, abstractmethod
from typing import Optional, Tuple

class Handler(ABC):
    def __init__(self, successor: Optional["Handler"] = None):
        self.successor = successor

    def handle(self, request: int) -> None:
        res = self.check_range(request)
        if not res and self.successor:
            self.successor.handle(request)

    @abstractmethod
    def check_range(self, request: int) -> Optional[bool]:
        """Compare passed value to predefined interval"""


class ConcreteHandler0(Handler):
    @staticmethod
    def check_range(request: int) -> Optional[bool]:
        if 0 <= request < 10:
            print(f"request {request} handled in handler 0")
            return True
        return None


class ConcreteHandler1(Handler):
    start, end = 10, 20

    def check_range(self, request: int) -> Optional[bool]:
        if self.start <= request < self.end:
            print(f"request {request} handled in handler 1")
            return True
        return None


class ConcreteHandler2(Handler):
    def check_range(self, request: int) -> Optional[bool]:
        start, end = self.get_interval_from_db()
        if start <= request < end:
            print(f"request {request} handled in handler 2")
            return True
        return None

    @staticmethod
    def get_interval_from_db() -> Tuple[int, int]:
        return (20, 30)


class FallbackHandler(Handler):
    @staticmethod
    def check_range(request: int) -> Optional[bool]:
        print(f"end of chain, no handler for {request}")
        return False
```

### Command

Object oriented implementation of callback functions.


```python
from typing import List, Union


class HideFileCommand:
    def __init__(self) -> None:
        self._hidden_files: List[str] = []

    def execute(self, filename: str) -> None:
        print(f"hiding {filename}")
        self._hidden_files.append(filename)

    def undo(self) -> None:
        filename = self._hidden_files.pop()
        print(f"un-hiding {filename}")


class DeleteFileCommand:
    def __init__(self) -> None:
        self._deleted_files: List[str] = []

    def execute(self, filename: str) -> None:
        print(f"deleting {filename}")
        self._deleted_files.append(filename)

    def undo(self) -> None:
        filename = self._deleted_files.pop()
        print(f"restoring {filename}")


class MenuItem:
    def __init__(self, command: Union[HideFileCommand, DeleteFileCommand]) -> None:
        self._command = command

    def on_do_press(self, filename: str) -> None:
        self._command.execute(filename)

    def on_undo_press(self) -> None:
        self._command.undo()
```

### Iterator

Traverses a container and accesses the container's elements.

```python

def count_to(count: int):
    numbers = ["one", "two", "three", "four", "five"]
    yield from numbers[:count]


def count_to_two() -> None:
    return count_to(2)


def count_to_five() -> None:
    return count_to(5)
```

Implementation of the iterator pattern using the iterator protocol from Python.
Traverses a container and accesses the container's elements.

```python
from __future__ import annotations


class NumberWords:
    _WORD_MAP = (
        "one",
        "two",
        "three",
        "four",
        "five",
    )

    def __init__(self, start: int, stop: int) -> None:
        self.start = start
        self.stop = stop

    def __iter__(self) -> NumberWords:
        return self

    def __next__(self) -> str:
        if self.start > self.stop or self.start > len(self._WORD_MAP):
            raise StopIteration
        current = self.start
        self.start += 1
        return self._WORD_MAP[current - 1]
```


### Mediator

Encapsulates how a set of objects interact.

```python

from __future__ import annotations


class ChatRoom:
    def display_message(self, user: User, message: str) -> None:
        print(f"[{user} says]: {message}")


class User:
    def __init__(self, name: str) -> None:
        self.name = name
        self.chat_room = ChatRoom()

    def say(self, message: str) -> None:
        self.chat_room.display_message(self, message)

    def __str__(self) -> str:
        return self.name
```

### Memento

Provides the ability to restore an object to its previous state.

```python
from typing import Callable, List
from copy import copy, deepcopy


def memento(obj, deep=False):
    state = deepcopy(obj.__dict__) if deep else copy(obj.__dict__)

    def restore():
        obj.__dict__.clear()
        obj.__dict__.update(state)

    return restore


class Transaction:
    deep = False
    states: List[Callable[[], None]] = []

    def __init__(self, deep, *targets):
        self.deep = deep
        self.targets = targets
        self.commit()

    def commit(self):
        self.states = [memento(target, self.deep) for target in self.targets]

    def rollback(self):
        for a_state in self.states:
            a_state()


class Transactional:
    def __init__(self, method):
        self.method = method

    def __get__(self, obj, T):
        """
        A decorator that makes a function transactional.

        :param method: The function to be decorated.
        """

        def transaction(*args, **kwargs):
            state = memento(obj)
            try:
                return self.method(obj, *args, **kwargs)
            except Exception as e:
                state()
                raise e

        return transaction


class NumObj:
    def __init__(self, value):
        self.value = value

    def __repr__(self):
        return f"<{self.__class__.__name__}: {self.value!r}>"

    def increment(self):
        self.value += 1

    @Transactional
    def do_stuff(self):
        self.value = "1111"  
        self.increment()
```


### Observer

Maintains a list of dependents and notifies them of any state changes.

```python
from __future__ import annotations

from contextlib import suppress
from typing import Protocol


class Observer(Protocol):
    def update(self, subject: Subject) -> None:
        pass


class Subject:
    def __init__(self) -> None:
        self._observers: list[Observer] = []

    def attach(self, observer: Observer) -> None:
        if observer not in self._observers:
            self._observers.append(observer)

    def detach(self, observer: Observer) -> None:
        with suppress(ValueError):
            self._observers.remove(observer)

    def notify(self, modifier: Observer | None = None) -> None:
        for observer in self._observers:
            if modifier != observer:
                observer.update(self)


class Data(Subject):
    def __init__(self, name: str = "") -> None:
        super().__init__()
        self.name = name
        self._data = 0

    @property
    def data(self) -> int:
        return self._data

    @data.setter
    def data(self, value: int) -> None:
        self._data = value
        self.notify()


class HexViewer:
    def update(self, subject: Data) -> None:
        print(f"HexViewer: Subject {subject.name} has data 0x{subject.data:x}")


class DecimalViewer:
    def update(self, subject: Data) -> None:
        print(f"DecimalViewer: Subject {subject.name} has data {subject.data}")
```

### State Method

Implements state as a derived class of the state pattern interface.
Implements state transitions by invoking methods from the pattern's superclass.

```python
from __future__ import annotations


class State:
    def scan(self) -> None:
        self.pos += 1
        if self.pos == len(self.stations):
            self.pos = 0
        print(f"Scanning... Station is {self.stations[self.pos]} {self.name}")


class AmState(State):
    def __init__(self, radio: Radio) -> None:
        self.radio = radio
        self.stations = ["1250", "1380", "1510"]
        self.pos = 0
        self.name = "AM"

    def toggle_amfm(self) -> None:
        print("Switching to FM")
        self.radio.state = self.radio.fmstate


class FmState(State):
    def __init__(self, radio: Radio) -> None:
        self.radio = radio
        self.stations = ["81.3", "89.1", "103.9"]
        self.pos = 0
        self.name = "FM"

    def toggle_amfm(self) -> None:
        print("Switching to AM")
        self.radio.state = self.radio.amstate


class Radio:
    def __init__(self) -> None:
        self.amstate = AmState(self)
        self.fmstate = FmState(self)
        self.state = self.amstate

    def toggle_amfm(self) -> None:
        self.state.toggle_amfm()

    def scan(self) -> None:
        self.state.scan()
```


### Strategy

Enables selecting an algorithm at runtime.

```python
from __future__ import annotations

from typing import Callable


class DiscountStrategyValidator:  # Descriptor class for check perform
    @staticmethod
    def validate(obj: Order, value: Callable) -> bool:
        try:
            if obj.price - value(obj) < 0:
                raise ValueError(
                    f"Discount cannot be applied due to negative price resulting. {value.__name__}"
                )
        except ValueError as ex:
            print(str(ex))
            return False
        else:
            return True

    def __set_name__(self, owner, name: str) -> None:
        self.private_name = f"_{name}"

    def __set__(self, obj: Order, value: Callable = None) -> None:
        if value and self.validate(obj, value):
            setattr(obj, self.private_name, value)
        else:
            setattr(obj, self.private_name, None)

    def __get__(self, obj: object, objtype: type = None):
        return getattr(obj, self.private_name)


class Order:
    discount_strategy = DiscountStrategyValidator()

    def __init__(self, price: float, discount_strategy: Callable = None) -> None:
        self.price: float = price
        self.discount_strategy = discount_strategy

    def apply_discount(self) -> float:
        if self.discount_strategy:
            discount = self.discount_strategy(self)
        else:
            discount = 0

        return self.price - discount

    def __repr__(self) -> str:
        return f"<Order price: {self.price} with discount strategy: {getattr(self.discount_strategy,'__name__',None)}>"


def ten_percent_discount(order: Order) -> float:
    return order.price * 0.10


def on_sale_discount(order: Order) -> float:
    return order.price * 0.25 + 20
```

### Template

Defines the skeleton of a base algorithm, deferring definition of exact
steps to subclasses.

```python
def get_text() -> str:
    return "plain-text"


def get_pdf() -> str:
    return "pdf"


def get_csv() -> str:
    return "csv"


def convert_to_text(data: str) -> str:
    print("[CONVERT]")
    return f"{data} as text"


def saver() -> None:
    print("[SAVE]")


def template_function(getter, converter=False, to_save=False) -> None:
    data = getter()
    print(f"Got `{data}`")

    if len(data) <= 3 and converter:
        data = converter(data)
    else:
        print("Skip conversion")

    if to_save:
        saver()

    print(f"`{data}` was processed")

```

### Visitor

Separates an algorithm from an object structure on which it operates.

```python
class Node:
    pass


class A(Node):
    pass


class B(Node):
    pass


class C(A, B):
    pass


class Visitor:
    def visit(self, node, *args, **kwargs):
        meth = None
        for cls in node.__class__.__mro__:
            meth_name = "visit_" + cls.__name__
            meth = getattr(self, meth_name, None)
            if meth:
                break

        if not meth:
            meth = self.generic_visit
        return meth(node, *args, **kwargs)

    def generic_visit(self, node, *args, **kwargs):
        print("generic_visit " + node.__class__.__name__)

    def visit_B(self, node, *args, **kwargs):
        print("visit_B " + node.__class__.__name__)
```
## Test Automation

### Page object

The page object pattern intends to create an object for each part of a web page. This technique helps build a separation between the test code and the actual code that interacts with the web page.

```python
from element import BasePageElement
from locators import MainPageLocators

class SearchTextElement(BasePageElement):
    locator = 'q'


class BasePage(object):
    def __init__(self, driver):
        self.driver = driver


class MainPage(BasePage):
    search_text_element = SearchTextElement()

    def is_title_matches(self):
        return "Python" in self.driver.title

    def click_go_button(self):
        element = self.driver.find_element(*MainPageLocators.GO_BUTTON)
        element.click()


class SearchResultsPage(BasePage):
    def is_results_found(self):
        return "No results found." not in self.driver.page_source
```



## References
 - https://github.com/faif/python-patterns
 - https://selenium-python.readthedocs.io/page-objects.html
