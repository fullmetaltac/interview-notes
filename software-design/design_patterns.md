# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Creational Design Patterns](#creational-design-patterns)
    - [Factory Method](#factory-method)
    - [Abstract Factory Method](#abstract-factory-method)
    - [Builder Method](#builder-method)
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
    - [Strategy Method](#strategy-method)
    - [Template Method](#template-method)
    - [Visitor Method](#visitor-method)
  - [Others](#others)
    - [Dependency Injection](#dependency-injection)
    - [Page object](#page-object)
  - [References](#references)

Design Patterns is the most essential part of Software Engineering, as they provide the general repeatable solution to a commonly occurring problem in software design. They usually represent some of the best practices adopted by experienced object-oriented software developers. We can not consider the Design Patterns as the finished design that can be directly converted into code. They are only templates that describe how to solve a particular problem with great efficiency.

---
## Creational Design Patterns
Creational patterns provides essential information regarding the Class instantiation or the object instantiation. Class Creational Pattern and the Object Creational pattern is the major categorization of the Creational Design Patterns. While class-creation patterns use inheritance effectively in the instantiation process, object-creation patterns use delegation effectively to get the job done.

### Factory Method 
* What is this pattern about?
A Factory is an object for creating other objects.

* What does this example do?
The code shows a way to localize words in two languages: English and
Greek. `get_localizer` is the factory function that constructs a
localizer depending on the language chosen. The localizer object will
be an instance from a different class according to the language
localized. However, the main code does not have to worry about which
localizer will be instantiated, since the method `localize` will be called
in the same way independently of the language.

* Where can the pattern be used practically?
The Factory Method can be seen in the popular web framework Django:
https://docs.djangoproject.com/en/4.0/topics/forms/formsets/
For example, different types of forms are created using a formset_factory

* TL;DR
**Creates objects without having to specify the exact class.**

```python
from typing import Dict
from typing import Protocol
from typing import Type


class Localizer(Protocol):
    def localize(self, msg: str) -> str:
        pass


class GreekLocalizer:
    """A simple localizer a la gettext"""

    def __init__(self) -> None:
        self.translations = {"dog": "σκύλος", "cat": "γάτα"}

    def localize(self, msg: str) -> str:
        """We'll punt if we don't have a translation"""
        return self.translations.get(msg, msg)


class EnglishLocalizer:
    """Simply echoes the message"""

    def localize(self, msg: str) -> str:
        return msg


def get_localizer(language: str = "English") -> Localizer:
    """Factory"""
    localizers: Dict[str, Type[Localizer]] = {
        "English": EnglishLocalizer,
        "Greek": GreekLocalizer,
    }

    return localizers[language]()


def main():
    """
    # Create our localizers
    >>> e, g = get_localizer(language="English"), get_localizer(language="Greek")

    # Localize some text
    >>> for msg in "dog parrot cat bear".split():
    ...     print(e.localize(msg), g.localize(msg))
    dog σκύλος
    parrot parrot
    cat γάτα
    bear bear
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod()

```

### Abstract Factory Method 
* What is this pattern about?

    In Java and other languages, the Abstract Factory Pattern serves to provide an interface for
    creating related/dependent objects without need to specify their
    actual class.

    The idea is to abstract the creation of objects depending on business
    logic, platform choice, etc.

    In Python, the interface we use is simply a callable, which is "builtin" interface
    in Python, and in normal circumstances we can simply use the class itself as
    that callable, because classes are first class objects in Python.

* What does this example do?
This particular implementation abstracts the creation of a pet and
does so depending on the factory we chose (Dog or Cat, or random_animal)
This works because both Dog/Cat and random_animal respect a common
interface (callable for creation and .speak()).
Now my application can create pets abstractly and decide later,
based on my own criteria, dogs over cats.

* TL;DR
**Provides a way to encapsulate a group of individual factories.**

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

    """A pet shop"""

    def __init__(self, animal_factory: Type[Pet]) -> None:
        """pet_factory is our abstract factory.  We can set it at will."""

        self.pet_factory = animal_factory

    def buy_pet(self, name: str) -> Pet:
        """Creates and shows a pet using the abstract factory"""

        pet = self.pet_factory(name)
        print(f"Here is your lovely {pet}")
        return pet


# Additional factories:

# Create a random animal
def random_animal(name: str) -> Pet:
    """Let's be dynamic!"""
    return random.choice([Dog, Cat])(name)


# Show pets with various factories
def main() -> None:
    """
    # A Shop that sells only cats
    >>> cat_shop = PetShop(Cat)
    >>> pet = cat_shop.buy_pet("Lucy")
    Here is your lovely Cat<Lucy>
    >>> pet.speak()
    meow

    # A shop that sells random animals
    >>> shop = PetShop(random_animal)
    >>> for name in ["Max", "Jack", "Buddy"]:
    ...    pet = shop.buy_pet(name)
    ...    pet.speak()
    ...    print("=" * 20)
    Here is your lovely Cat<Max>
    meow
    ====================
    Here is your lovely Dog<Jack>
    woof
    ====================
    Here is your lovely Dog<Buddy>
    woof
    ====================
    """


if __name__ == "__main__":
    random.seed(1234)  # for deterministic doctest outputs
    shop = PetShop(random_animal)
    import doctest

    doctest.testmod()
```

### Builder Method
* What is this pattern about?
It decouples the creation of a complex object and its representation,
so that the same process can be reused to build objects from the same
family.
This is useful when you must separate the specification of an object
from its actual representation (generally for abstraction).

* What does this example do?

    The first example achieves this by using an abstract base
    class for a building, where the initializer (`__init__` method) specifies the
    steps needed, and the concrete subclasses implement these steps.

    In other programming languages, a more complex arrangement is sometimes
    necessary. In particular, you cannot have polymorphic behavior in a constructor in C++.
    Which means this Python technique will not work. The polymorphism
    required has to be provided by an external, already constructed
    instance of a different class.

    In general, in Python this won't be necessary, but a second example showing
    this kind of arrangement is also included.

* TL;DR
**Decouples the creation of a complex object and its representation.**

```python
# Abstract Building
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


# Concrete Buildings
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


# In some very complex cases, it might be desirable to pull out the building
# logic into another function (or a method on another class), rather than being
# in the base class '__init__'. (This leaves you in the strange situation where
# a concrete class does not have a useful constructor)


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


def main():
    """
    >>> house = House()
    >>> house
    Floor: One | Size: Big

    >>> flat = Flat()
    >>> flat
    Floor: More than One | Size: Small

    # Using an external constructor function:
    >>> complex_house = construct_building(ComplexHouse)
    >>> complex_house
    Floor: One | Size: Big and fancy
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Prototype
* What is this pattern about?
This patterns aims to reduce the number of classes required by an
application. Instead of relying on subclasses it creates objects by
copying a prototypical instance at run-time.

    This is useful as it makes it easier to derive new kinds of objects,
    when instances of the class have only a few different combinations of
    state, and when instantiation is expensive.

* What does this example do?
When the number of prototypes in an application can vary, it can be
useful to keep a Dispatcher (aka, Registry or Manager). This allows
clients to query the Dispatcher for a prototype before cloning a new
instance.

    Below provides an example of such Dispatcher, which contains three
    copies of the prototype: `default`, `objecta` and `objectb`.

*TL;DR
**Creates new object instances by cloning prototype.**

```python
from __future__ import annotations

from typing import Any


class Prototype:
    def __init__(self, value: str = "default", **attrs: Any) -> None:
        self.value = value
        self.__dict__.update(attrs)

    def clone(self, **attrs: Any) -> Prototype:
        """Clone a prototype and update inner attributes dictionary"""
        # Python in Practice, Mark Summerfield
        # copy.deepcopy can be used instead of next line.
        obj = self.__class__(**self.__dict__)
        obj.__dict__.update(attrs)
        return obj


class PrototypeDispatcher:
    def __init__(self):
        self._objects = {}

    def get_objects(self) -> dict[str, Prototype]:
        """Get all objects"""
        return self._objects

    def register_object(self, name: str, obj: Prototype) -> None:
        """Register an object"""
        self._objects[name] = obj

    def unregister_object(self, name: str) -> None:
        """Unregister an object"""
        del self._objects[name]


def main() -> None:
    """
    >>> dispatcher = PrototypeDispatcher()
    >>> prototype = Prototype()

    >>> d = prototype.clone()
    >>> a = prototype.clone(value='a-value', category='a')
    >>> b = a.clone(value='b-value', is_checked=True)
    >>> dispatcher.register_object('objecta', a)
    >>> dispatcher.register_object('objectb', b)
    >>> dispatcher.register_object('default', d)

    >>> [{n: p.value} for n, p in dispatcher.get_objects().items()]
    [{'objecta': 'a-value'}, {'objectb': 'b-value'}, {'default': 'default'}]

    >>> print(b.category, b.is_checked)
    a True
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Singleton 
"""
* What is this pattern about?
The Borg pattern (also known as the Monostate pattern) is a way to
implement singleton behavior, but instead of having only one instance
of a class, there are multiple instances that share the same state. In
other words, the focus is on sharing state instead of sharing instance
identity.

* What does this example do?
To understand the implementation of this pattern in Python, it is
important to know that, in Python, instance attributes are stored in a
attribute dictionary called `__dict__`. Usually, each instance will have
its own dictionary, but the Borg pattern modifies this so that all
instances have the same dictionary.
In this example, the `__shared_state` attribute will be the dictionary
shared between all instances, and this is ensured by assigning
`__shared_state` to the `__dict__` variable when initializing a new
instance (i.e., in the `__init__` method). Other attributes are usually
added to the instance's attribute dictionary, but, since the attribute
dictionary itself is shared (which is `__shared_state`), all other
attributes will also be shared.

* Where is the pattern used practically?
Sharing state is useful in applications like managing database connections:
https://github.com/onetwopunch/pythonDbTemplate/blob/master/database.py

* TL;DR
**Provides singleton-like behavior sharing state between instances.**

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
            # initiate the first instance with default state
            if not hasattr(self, "state"):
                self.state = "Init"

    def __str__(self) -> str:
        return self.state


def main():
    """
    >>> rm1 = YourBorg()
    >>> rm2 = YourBorg()

    >>> rm1.state = 'Idle'
    >>> rm2.state = 'Running'

    >>> print('rm1: {0}'.format(rm1))
    rm1: Running
    >>> print('rm2: {0}'.format(rm2))
    rm2: Running

    # When the `state` attribute is modified from instance `rm2`,
    # the value of `state` in instance `rm1` also changes
    >>> rm2.state = 'Zombie'

    >>> print('rm1: {0}'.format(rm1))
    rm1: Zombie
    >>> print('rm2: {0}'.format(rm2))
    rm2: Zombie

    # Even though `rm1` and `rm2` share attributes, the instances are not the same
    >>> rm1 is rm2
    False

    # New instances also get the same shared state
    >>> rm3 = YourBorg()

    >>> print('rm1: {0}'.format(rm1))
    rm1: Zombie
    >>> print('rm2: {0}'.format(rm2))
    rm2: Zombie
    >>> print('rm3: {0}'.format(rm3))
    rm3: Zombie

    # A new instance can explicitly change the state during creation
    >>> rm4 = YourBorg('Running')

    >>> print('rm4: {0}'.format(rm4))
    rm4: Running

    # Existing instances reflect that change as well
    >>> print('rm3: {0}'.format(rm3))
    rm3: Running
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```
### Object Pool
* What is this pattern about?
This pattern is used when creating an object is costly (and they are
created frequently) but only a few are used at a time. With a Pool we
can manage those instances we have as of now by caching them. Now it
is possible to skip the costly creation of an object if one is
available in the pool.
A pool allows to 'check out' an inactive object and then to return it.
If none are available the pool creates one to provide without wait.

* What does this example do?
In this example queue.Queue is used to create the pool (wrapped in a
custom ObjectPool object to use with the with statement), and it is
populated with strings.
As we can see, the first string object put in "yam" is USED by the
with statement. But because it is released back into the pool
afterwards it is reused by the explicit call to sample_queue.get().
Same thing happens with "sam", when the ObjectPool created inside the
function is deleted (by the GC) and the object is returned.

*TL;DR
**Stores a set of initialized objects kept ready to use.**

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


def main():
    """
    >>> import queue

    >>> def test_object(queue):
    ...    pool = ObjectPool(queue, True)
    ...    print('Inside func: {}'.format(pool.item))

    >>> sample_queue = queue.Queue()

    >>> sample_queue.put('yam')
    >>> with ObjectPool(sample_queue) as obj:
    ...    print('Inside with: {}'.format(obj))
    Inside with: yam

    >>> print('Outside with: {}'.format(sample_queue.get()))
    Outside with: yam

    >>> sample_queue.put('sam')
    >>> test_object(sample_queue)
    Inside func: sam

    >>> print('Outside func: {}'.format(sample_queue.get()))
    Outside func: sam

    if not sample_queue.empty():
        print(sample_queue.get())
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```


### Lazy Evaluation
Lazily-evaluated property pattern in Python.

https://en.wikipedia.org/wiki/Lazy_evaluation

* TL;DR
**Delays the eval of an expr until its value is needed and avoids repeated evals.**
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
    """
    A lazy property decorator.

    The function decorated is called the first time to retrieve the result and
    then that calculated result is used the next time you access the value.
    """
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
        # Get all relatives, let's assume that it costs much time.
        relatives = "Many relatives."
        return relatives

    @lazy_property2
    def parents(self):
        self.call_count2 += 1
        return "Father and mother"


def main():
    """
    >>> Jhon = Person('Jhon', 'Coder')

    >>> Jhon.name
    'Jhon'
    >>> Jhon.occupation
    'Coder'

    # Before we access `relatives`
    >>> sorted(Jhon.__dict__.items())
    [('call_count2', 0), ('name', 'Jhon'), ('occupation', 'Coder')]

    >>> Jhon.relatives
    'Many relatives.'

    # After we've accessed `relatives`
    >>> sorted(Jhon.__dict__.items())
    [('call_count2', 0), ..., ('relatives', 'Many relatives.')]

    >>> Jhon.parents
    'Father and mother'

    >>> sorted(Jhon.__dict__.items())
    [('_lazy__parents', 'Father and mother'), ('call_count2', 1), ..., ('relatives', 'Many relatives.')]

    >>> Jhon.parents
    'Father and mother'

    >>> Jhon.call_count2
    1
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

---
## Structural Design Patterns
Structural design patterns are about organizing different classes and objects to form larger structures and provide new functionality while keeping these structures flexible and efficient. Mostly they use Inheritance to compose all the interfaces. It also identifies the relationships which led to the simplification of the structure.

### Adapter
* What is this pattern about?
The Adapter pattern provides a different interface for a class. We can
think about it as a cable adapter that allows you to charge a phone
somewhere that has outlets in a different shape. Following this idea,
the Adapter pattern is useful to integrate classes that couldn't be
integrated due to their incompatible interfaces.

* What does this example do?

    The example has classes that represent entities (Dog, Cat, Human, Car)
    that make different noises. The Adapter class provides a different
    interface to the original methods that make such noises. So the
    original interfaces (e.g., bark and meow) are available under a
    different name: make_noise.

* Where is the pattern used practically?
The Grok framework uses adapters to make objects work with a
particular API without modifying the objects themselves:
http://grok.zope.org/doc/current/grok_overview.html#adapters

* TL;DR
**Allows the interface of an existing class to be used as another interface.**

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
    """Adapts an object by replacing methods.

    Usage
    ------
    dog = Dog()
    dog = Adapter(dog, make_noise=dog.bark)
    """

    def __init__(self, obj: T, **adapted_methods: Callable):
        """We set the adapted methods in the object's dict."""
        self.obj = obj
        self.__dict__.update(adapted_methods)

    def __getattr__(self, attr):
        """All non-adapted calls are passed to the object."""
        return getattr(self.obj, attr)

    def original_dict(self):
        """Print original object dict."""
        return self.obj.__dict__


def main():
    """
    >>> objects = []
    >>> dog = Dog()
    >>> print(dog.__dict__)
    {'name': 'Dog'}

    >>> objects.append(Adapter(dog, make_noise=dog.bark))

    >>> objects[0].__dict__['obj'], objects[0].__dict__['make_noise']
    (<...Dog object at 0x...>, <bound method Dog.bark of <...Dog object at 0x...>>)

    >>> print(objects[0].original_dict())
    {'name': 'Dog'}

    >>> cat = Cat()
    >>> objects.append(Adapter(cat, make_noise=cat.meow))
    >>> human = Human()
    >>> objects.append(Adapter(human, make_noise=human.speak))
    >>> car = Car()
    >>> objects.append(Adapter(car, make_noise=lambda: car.make_noise(3)))

    >>> for obj in objects:
    ...    print("A {0} goes {1}".format(obj.name, obj.make_noise()))
    A Dog goes woof!
    A Cat goes meow!
    A Human goes 'hello'
    A Car goes vroom!!!
    """


if __name__ == "__main__":
    import doctest
    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

### Bridge
* References:
http://en.wikibooks.org/wiki/Computer_Science_Design_Patterns/Bridge_Pattern#Python

* TL;DR
**Decouples an abstraction from its implementation.**

```python
# ConcreteImplementor 1/2
class DrawingAPI1:
    def draw_circle(self, x, y, radius):
        print(f"API1.circle at {x}:{y} radius {radius}")


# ConcreteImplementor 2/2
class DrawingAPI2:
    def draw_circle(self, x, y, radius):
        print(f"API2.circle at {x}:{y} radius {radius}")


# Refined Abstraction
class CircleShape:
    def __init__(self, x, y, radius, drawing_api):
        self._x = x
        self._y = y
        self._radius = radius
        self._drawing_api = drawing_api

    # low-level i.e. Implementation specific
    def draw(self):
        self._drawing_api.draw_circle(self._x, self._y, self._radius)

    # high-level i.e. Abstraction specific
    def scale(self, pct):
        self._radius *= pct


def main():
    """
    >>> shapes = (CircleShape(1, 2, 3, DrawingAPI1()), CircleShape(5, 7, 11, DrawingAPI2()))

    >>> for shape in shapes:
    ...    shape.scale(2.5)
    ...    shape.draw()
    API1.circle at 1:2 radius 7.5
    API2.circle at 5:7 radius 27.5
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Composite
* What is this pattern about?
The composite pattern describes a group of objects that is treated the
same way as a single instance of the same type of object. The intent of
a composite is to "compose" objects into tree structures to represent
part-whole hierarchies. Implementing the composite pattern lets clients
treat individual objects and compositions uniformly.

* What does this example do?
The example implements a graphic class，which can be either an ellipse
or a composition of several graphics. Every graphic can be printed.

* Where is the pattern used practically?
In graphics editors a shape can be basic or complex. An example of a
simple shape is a line, where a complex shape is a rectangle which is
made of four line objects. Since shapes have many operations in common
such as rendering the shape to screen, and since shapes follow a
part-whole hierarchy, composite pattern can be used to enable the
program to deal with all shapes uniformly.

* TL;DR
**Describes a group of objects that is treated as a single instance.**

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


def main():
    """
    >>> ellipse1 = Ellipse("1")
    >>> ellipse2 = Ellipse("2")
    >>> ellipse3 = Ellipse("3")
    >>> ellipse4 = Ellipse("4")

    >>> graphic1 = CompositeGraphic()
    >>> graphic2 = CompositeGraphic()

    >>> graphic1.add(ellipse1)
    >>> graphic1.add(ellipse2)
    >>> graphic1.add(ellipse3)
    >>> graphic2.add(ellipse4)

    >>> graphic = CompositeGraphic()

    >>> graphic.add(graphic1)
    >>> graphic.add(graphic2)

    >>> graphic.render()
    Ellipse: 1
    Ellipse: 2
    Ellipse: 3
    Ellipse: 4
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Decorator
* What is this pattern about?
The Decorator pattern is used to dynamically add a new feature to an
object without changing its implementation. It differs from
inheritance because the new feature is added only to that particular
object, not to the entire subclass.

* What does this example do?
This example shows a way to add formatting options (boldface and
italic) to a text by appending the corresponding tags (`<b>` and
`<i>`). Also, we can see that decorators can be applied one after the other,
since the original text is passed to the bold wrapper, which in turn
is passed to the italic wrapper.

* Where is the pattern used practically?
The Grok framework uses decorators to add functionalities to methods,
like permissions or subscription to an event:
http://grok.zope.org/doc/current/reference/decorators.html

* TL;DR
**Adds behaviour to object without affecting its class.**

```python
class TextTag:
    """Represents a base text tag"""

    def __init__(self, text: str) -> None:
        self._text = text

    def render(self) -> str:
        return self._text


class BoldWrapper(TextTag):
    """Wraps a tag in <b>"""

    def __init__(self, wrapped: TextTag) -> None:
        self._wrapped = wrapped

    def render(self) -> str:
        return f"<b>{self._wrapped.render()}</b>"


class ItalicWrapper(TextTag):
    """Wraps a tag in <i>"""

    def __init__(self, wrapped: TextTag) -> None:
        self._wrapped = wrapped

    def render(self) -> str:
        return f"<i>{self._wrapped.render()}</i>"


def main():
    """
    >>> simple_hello = TextTag("hello, world!")
    >>> special_hello = ItalicWrapper(BoldWrapper(simple_hello))

    >>> print("before:", simple_hello.render())
    before: hello, world!

    >>> print("after:", special_hello.render())
    after: <i><b>hello, world!</b></i>
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```
### Facade
* Example from https://en.wikipedia.org/wiki/Facade_pattern#Python

* What is this pattern about?
The Facade pattern is a way to provide a simpler unified interface to
a more complex system. It provides an easier way to access functions
of the underlying system by providing a single entry point.
This kind of abstraction is seen in many real life situations. For
example, we can turn on a computer by just pressing a button, but in
fact there are many procedures and operations done when that happens
(e.g., loading programs from disk to memory). In this case, the button
serves as an unified interface to all the underlying procedures to
turn on a computer.

* Where is the pattern used practically?
This pattern can be seen in the Python standard library when we use
the `isdir` function. Although a user simply uses this function to know
whether a path refers to a directory, the system makes a few
operations and calls other modules (e.g., os.stat) to give the result.

* TL;DR
**Provides a simpler unified interface to a complex system.**

```python
# Complex computer parts
class CPU:
    """
    Simple CPU representation.
    """

    def freeze(self) -> None:
        print("Freezing processor.")

    def jump(self, position: str) -> None:
        print("Jumping to:", position)

    def execute(self) -> None:
        print("Executing.")


class Memory:
    """
    Simple memory representation.
    """

    def load(self, position: str, data: str) -> None:
        print(f"Loading from {position} data: '{data}'.")


class SolidStateDrive:
    """
    Simple solid state drive representation.
    """

    def read(self, lba: str, size: str) -> str:
        return f"Some data from sector {lba} with size {size}"


class ComputerFacade:
    """
    Represents a facade for various computer parts.
    """

    def __init__(self):
        self.cpu = CPU()
        self.memory = Memory()
        self.ssd = SolidStateDrive()

    def start(self):
        self.cpu.freeze()
        self.memory.load("0x00", self.ssd.read("100", "1024"))
        self.cpu.jump("0x00")
        self.cpu.execute()


def main():
    """
    >>> computer_facade = ComputerFacade()
    >>> computer_facade.start()
    Freezing processor.
    Loading from 0x00 data: 'Some data from sector 100 with size 1024'.
    Jumping to: 0x00
    Executing.
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod(optionflags=doctest.ELLIPSIS)
```


### Flyweight
* What is this pattern about?
This pattern aims to minimise the number of objects that are needed by
a program at run-time. A Flyweight is an object shared by multiple
contexts, and is indistinguishable from an object that is not shared.

    The state of a Flyweight should not be affected by it's context, this
    is known as its intrinsic state. The decoupling of the objects state
    from the object's context, allows the Flyweight to be shared.

* What does this example do?
The example below sets-up an 'object pool' which stores initialised
objects. When a 'Card' is created it first checks to see if it already
exists instead of creating a new one. This aims to reduce the number of
objects initialised by the program.

* Examples in Python ecosystem:
https://docs.python.org/3/library/sys.html#sys.intern

* TL;DR
**Minimizes memory usage by sharing data with other similar objects.**

```python
import weakref


class Card:
    """The Flyweight"""

    # Could be a simple dict.
    # With WeakValueDictionary garbage collection can reclaim the object
    # when there are no other references to it.
    _pool: weakref.WeakValueDictionary = weakref.WeakValueDictionary()

    def __new__(cls, value, suit):
        # If the object exists in the pool - just return it
        obj = cls._pool.get(value + suit)
        # otherwise - create new one (and add it to the pool)
        if obj is None:
            obj = object.__new__(Card)
            cls._pool[value + suit] = obj
            # This row does the part we usually see in `__init__`
            obj.value, obj.suit = value, suit
        return obj

    # If you uncomment `__init__` and comment-out `__new__` -
    #   Card becomes normal (non-flyweight).
    # def __init__(self, value, suit):
    #     self.value, self.suit = value, suit

    def __repr__(self):
        return f"<Card: {self.value}{self.suit}>"


def main():
    """
    >>> c1 = Card('9', 'h')
    >>> c2 = Card('9', 'h')
    >>> c1, c2
    (<Card: 9h>, <Card: 9h>)
    >>> c1 == c2
    True
    >>> c1 is c2
    True

    >>> c1.new_attr = 'temp'
    >>> c3 = Card('9', 'h')
    >>> hasattr(c3, 'new_attr')
    True

    >>> Card._pool.clear()
    >>> c4 = Card('9', 'h')
    >>> hasattr(c4, 'new_attr')
    False
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

**Flyweight with metaclass**
```python
import weakref


class FlyweightMeta(type):
    def __new__(mcs, name, parents, dct):
        """
        Set up object pool

        :param name: class name
        :param parents: class parents
        :param dct: dict: includes class attributes, class methods,
        static methods, etc
        :return: new class
        """
        dct["pool"] = weakref.WeakValueDictionary()
        return super().__new__(mcs, name, parents, dct)

    @staticmethod
    def _serialize_params(cls, *args, **kwargs):
        """
        Serialize input parameters to a key.
        Simple implementation is just to serialize it as a string
        """
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


if __name__ == "__main__":
    instances_pool = getattr(Card2, "pool")
    cm1 = Card2("10", "h", a=1)
    cm2 = Card2("10", "h", a=1)
    cm3 = Card2("10", "h", a=2)

    assert (cm1 == cm2) and (cm1 != cm3)
    assert (cm1 is cm2) and (cm1 is not cm3)
    assert len(instances_pool) == 2

    del cm1
    assert len(instances_pool) == 2

    del cm2
    assert len(instances_pool) == 1

    del cm3
    assert len(instances_pool) == 0
```


### Proxy 
* What is this pattern about?
Proxy is used in places where you want to add functionality to a class without
changing its interface. The main class is called `Real Subject`. A client should
use the proxy or the real subject without any code change, so both must have the
same interface. Logging and controlling access to the real subject are some of
the proxy pattern usages.

* TL;DR
Add functionality or logic (e.g. logging, caching, authorization) to a resource
without changing its interface.

```python
from typing import Union


class Subject:
    """
    As mentioned in the document, interfaces of both RealSubject and Proxy should
    be the same, because the client should be able to use RealSubject or Proxy with
    no code change.

    Not all times this interface is necessary. The point is the client should be
    able to use RealSubject or Proxy interchangeably with no change in code.
    """

    def do_the_job(self, user: str) -> None:
        raise NotImplementedError()


class RealSubject(Subject):
    """
    This is the main job doer. External services like payment gateways can be a
    good example.
    """

    def do_the_job(self, user: str) -> None:
        print(f"I am doing the job for {user}")


class Proxy(Subject):
    def __init__(self) -> None:
        self._real_subject = RealSubject()

    def do_the_job(self, user: str) -> None:
        """
        logging and controlling access are some examples of proxy usages.
        """

        print(f"[log] Doing the job for {user} is requested.")

        if user == "admin":
            self._real_subject.do_the_job(user)
        else:
            print("[log] I can do the job just for `admins`.")


def client(job_doer: Union[RealSubject, Proxy], user: str) -> None:
    job_doer.do_the_job(user)


def main():
    """
    >>> proxy = Proxy()

    >>> real_subject = RealSubject()

    >>> client(proxy, 'admin')
    [log] Doing the job for admin is requested.
    I am doing the job for admin

    >>> client(proxy, 'anonymous')
    [log] Doing the job for anonymous is requested.
    [log] I can do the job just for `admins`.

    >>> client(real_subject, 'admin')
    I am doing the job for admin

    >>> client(real_subject, 'anonymous')
    I am doing the job for anonymous
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

---
## Behavioral Design Pattern
Behavioral patterns are all about identifying the common communication patterns between objects and realize these patterns. These patterns are concerned with algorithms and the assignment of responsibilities between objects.

### Chain of Responsibility
* What is this pattern about?

    The Chain of responsibility is an object oriented version of the
    `if ... elif ... elif ... else ...` idiom, with the
    benefit that the condition–action blocks can be dynamically rearranged
    and reconfigured at runtime.

    This pattern aims to decouple the senders of a request from its
    receivers by allowing request to move through chained
    receivers until it is handled.

    Request receiver in simple form keeps a reference to a single successor.
    As a variation some receivers may be capable of sending requests out
    in several directions, forming a `tree of responsibility`.

* TL;DR
Allow a request to pass down a chain of receivers until it is handled.

```python
from abc import ABC, abstractmethod
from typing import Optional, Tuple

class Handler(ABC):
    def __init__(self, successor: Optional["Handler"] = None):
        self.successor = successor

    def handle(self, request: int) -> None:
        """
        Handle request and stop.
        If can't - call next handler in chain.

        As an alternative you might even in case of success
        call the next handler.
        """
        res = self.check_range(request)
        if not res and self.successor:
            self.successor.handle(request)

    @abstractmethod
    def check_range(self, request: int) -> Optional[bool]:
        """Compare passed value to predefined interval"""


class ConcreteHandler0(Handler):
    """Each handler can be different.
    Be simple and static...
    """

    @staticmethod
    def check_range(request: int) -> Optional[bool]:
        if 0 <= request < 10:
            print(f"request {request} handled in handler 0")
            return True
        return None


class ConcreteHandler1(Handler):
    """... With it's own internal state"""

    start, end = 10, 20

    def check_range(self, request: int) -> Optional[bool]:
        if self.start <= request < self.end:
            print(f"request {request} handled in handler 1")
            return True
        return None


class ConcreteHandler2(Handler):
    """... With helper methods."""

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


def main():
    """
    >>> h0 = ConcreteHandler0()
    >>> h1 = ConcreteHandler1()
    >>> h2 = ConcreteHandler2(FallbackHandler())
    >>> h0.successor = h1
    >>> h1.successor = h2

    >>> requests = [2, 5, 14, 22, 18, 3, 35, 27, 20]
    >>> for request in requests:
    ...     h0.handle(request)
    request 2 handled in handler 0
    request 5 handled in handler 0
    request 14 handled in handler 1
    request 22 handled in handler 2
    request 18 handled in handler 1
    request 3 handled in handler 0
    end of chain, no handler for 35
    request 27 handled in handler 2
    request 20 handled in handler 2
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

### Command
* What is this pattern about?
Command pattern decouples the object invoking a job from the one who knows
how to do it. As mentioned in the GoF book, a good example is in menu items.
You have a menu that has lots of items. Each item is responsible for doing a
special thing and you want your menu item just call the execute method when
it is pressed. To achieve this you implement a command object with the execute
method for each menu item and pass to it.

* About the example
We have a menu containing two items. Each item accepts a file name, one hides the file
and the other deletes it. Both items have an undo option.
Each item is a MenuItem class that accepts the corresponding command as input and executes
it's execute method when it is pressed.

* Examples in Python ecosystem:
Django HttpRequest (without execute method):
https://docs.djangoproject.com/en/2.1/ref/request-response/#httprequest-objects


* TL;DR
**Object oriented implementation of callback functions.**


```python
from typing import List, Union


class HideFileCommand:
    """
    A command to hide a file given its name
    """

    def __init__(self) -> None:
        # an array of files hidden, to undo them as needed
        self._hidden_files: List[str] = []

    def execute(self, filename: str) -> None:
        print(f"hiding {filename}")
        self._hidden_files.append(filename)

    def undo(self) -> None:
        filename = self._hidden_files.pop()
        print(f"un-hiding {filename}")


class DeleteFileCommand:
    """
    A command to delete a file given its name
    """

    def __init__(self) -> None:
        # an array of deleted files, to undo them as needed
        self._deleted_files: List[str] = []

    def execute(self, filename: str) -> None:
        print(f"deleting {filename}")
        self._deleted_files.append(filename)

    def undo(self) -> None:
        filename = self._deleted_files.pop()
        print(f"restoring {filename}")


class MenuItem:
    """
    The invoker class. Here it is items in a menu.
    """

    def __init__(self, command: Union[HideFileCommand, DeleteFileCommand]) -> None:
        self._command = command

    def on_do_press(self, filename: str) -> None:
        self._command.execute(filename)

    def on_undo_press(self) -> None:
        self._command.undo()


def main():
    """
    >>> item1 = MenuItem(DeleteFileCommand())

    >>> item2 = MenuItem(HideFileCommand())

    # create a file named `test-file` to work with
    >>> test_file_name = 'test-file'

    # deleting `test-file`
    >>> item1.on_do_press(test_file_name)
    deleting test-file

    # restoring `test-file`
    >>> item1.on_undo_press()
    restoring test-file

    # hiding `test-file`
    >>> item2.on_do_press(test_file_name)
    hiding test-file

    # un-hiding `test-file`
    >>> item2.on_undo_press()
    un-hiding test-file
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Iterator
http://ginstrom.com/scribbles/2007/10/08/design-patterns-python-style/
Implementation of the iterator pattern with a generator

* TL;DR
**Traverses a container and accesses the container's elements.**
```python

def count_to(count: int):
    """Counts by word numbers, up to a maximum of five"""
    numbers = ["one", "two", "three", "four", "five"]
    yield from numbers[:count]


# Test the generator
def count_to_two() -> None:
    return count_to(2)


def count_to_five() -> None:
    return count_to(5)


def main():
    """
    # Counting to two...
    >>> for number in count_to_two():
    ...     print(number)
    one
    two

    # Counting to five...
    >>> for number in count_to_five():
    ...     print(number)
    one
    two
    three
    four
    five
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

Implementation of the iterator pattern using the iterator protocol from Python.
Traverses a container and accesses the container's elements.

```python
from __future__ import annotations


class NumberWords:
    """Counts by word numbers, up to a maximum of five"""

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

    def __iter__(self) -> NumberWords:  # this makes the class an Iterable
        return self

    def __next__(self) -> str:  # this makes the class an Iterator
        if self.start > self.stop or self.start > len(self._WORD_MAP):
            raise StopIteration
        current = self.start
        self.start += 1
        return self._WORD_MAP[current - 1]


# Test the iterator


def main():
    """
    # Counting to two...
    >>> for number in NumberWords(start=1, stop=2):
    ...     print(number)
    one
    two

    # Counting to five...
    >>> for number in NumberWords(start=1, stop=5):
    ...     print(number)
    one
    two
    three
    four
    five
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```


### Mediator
https://www.djangospin.com/design-patterns-python/mediator/

Objects in a system communicate through a Mediator instead of directly with each other.
This reduces the dependencies between communicating objects, thereby reducing coupling.

* TL;DR
**Encapsulates how a set of objects interact.**

```python

from __future__ import annotations


class ChatRoom:
    """Mediator class"""

    def display_message(self, user: User, message: str) -> None:
        print(f"[{user} says]: {message}")


class User:
    """A class whose instances want to interact with each other"""

    def __init__(self, name: str) -> None:
        self.name = name
        self.chat_room = ChatRoom()

    def say(self, message: str) -> None:
        self.chat_room.display_message(self, message)

    def __str__(self) -> str:
        return self.name


def main():
    """
    >>> molly = User('Molly')
    >>> mark = User('Mark')
    >>> ethan = User('Ethan')

    >>> molly.say("Hi Team! Meeting at 3 PM today.")
    [Molly says]: Hi Team! Meeting at 3 PM today.
    >>> mark.say("Roger that!")
    [Mark says]: Roger that!
    >>> ethan.say("Alright.")
    [Ethan says]: Alright.
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Memento
http://code.activestate.com/recipes/413838-memento-closure/

* TL;DR
**Provides the ability to restore an object to its previous state.**
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
    """A transaction guard.

    This is, in fact, just syntactic sugar around a memento closure.
    """

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
    """Adds transactional semantics to methods. Methods decorated  with

    @Transactional will rollback to entry-state upon exceptions.
    """

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
        self.value = "1111"  # <- invalid value
        self.increment()  # <- will fail and rollback


def main():
    """
    >>> num_obj = NumObj(-1)
    >>> print(num_obj)
    <NumObj: -1>

    >>> a_transaction = Transaction(True, num_obj)

    >>> try:
    ...    for i in range(3):
    ...        num_obj.increment()
    ...        print(num_obj)
    ...    a_transaction.commit()
    ...    print('-- committed')
    ...    for i in range(3):
    ...        num_obj.increment()
    ...        print(num_obj)
    ...    num_obj.value += 'x'  # will fail
    ...    print(num_obj)
    ... except Exception:
    ...    a_transaction.rollback()
    ...    print('-- rolled back')
    <NumObj: 0>
    <NumObj: 1>
    <NumObj: 2>
    -- committed
    <NumObj: 3>
    <NumObj: 4>
    <NumObj: 5>
    -- rolled back

    >>> print(num_obj)
    <NumObj: 2>

    >>> print('-- now doing stuff ...')
    -- now doing stuff ...

    >>> try:
    ...    num_obj.do_stuff()
    ... except Exception:
    ...    print('-> doing stuff failed!')
    ...    import sys
    ...    import traceback
    ...    traceback.print_exc(file=sys.stdout)
    -> doing stuff failed!
    Traceback (most recent call last):
    ...
    TypeError: ...str...int...

    >>> print(num_obj)
    <NumObj: 2>
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod(optionflags=doctest.ELLIPSIS)
```


### Observer
http://code.activestate.com/recipes/131499-observer-pattern/

* Examples in Python ecosystem:
Django Signals: https://docs.djangoproject.com/en/3.1/topics/signals/
Flask Signals: https://flask.palletsprojects.com/en/1.1.x/signals/


* TL;DR
Maintains a list of dependents and notifies them of any state changes.

```python
from __future__ import annotations

from contextlib import suppress
from typing import Protocol


# define a generic observer type
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


def main():
    """
    >>> data1 = Data('Data 1')
    >>> data2 = Data('Data 2')
    >>> view1 = DecimalViewer()
    >>> view2 = HexViewer()
    >>> data1.attach(view1)
    >>> data1.attach(view2)
    >>> data2.attach(view2)
    >>> data2.attach(view1)

    >>> data1.data = 10
    DecimalViewer: Subject Data 1 has data 10
    HexViewer: Subject Data 1 has data 0xa

    >>> data2.data = 15
    HexViewer: Subject Data 2 has data 0xf
    DecimalViewer: Subject Data 2 has data 15

    >>> data1.data = 3
    DecimalViewer: Subject Data 1 has data 3
    HexViewer: Subject Data 1 has data 0x3

    >>> data2.data = 5
    HexViewer: Subject Data 2 has data 0x5
    DecimalViewer: Subject Data 2 has data 5

    # Detach HexViewer from data1 and data2
    >>> data1.detach(view2)
    >>> data2.detach(view2)

    >>> data1.data = 10
    DecimalViewer: Subject Data 1 has data 10

    >>> data2.data = 15
    DecimalViewer: Subject Data 2 has data 15
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### State Method
Implementation of the state pattern

http://ginstrom.com/scribbles/2007/10/08/design-patterns-python-style/

* TL;DR
Implements state as a derived class of the state pattern interface.
Implements state transitions by invoking methods from the pattern's superclass.

```python
from __future__ import annotations


class State:
    """Base state. This is to share functionality"""

    def scan(self) -> None:
        """Scan the dial to the next station"""
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
    """A radio.     It has a scan button, and an AM/FM toggle switch."""

    def __init__(self) -> None:
        """We have an AM state and an FM state"""
        self.amstate = AmState(self)
        self.fmstate = FmState(self)
        self.state = self.amstate

    def toggle_amfm(self) -> None:
        self.state.toggle_amfm()

    def scan(self) -> None:
        self.state.scan()


def main():
    """
    >>> radio = Radio()
    >>> actions = [radio.scan] * 2 + [radio.toggle_amfm] + [radio.scan] * 2
    >>> actions *= 2

    >>> for action in actions:
    ...    action()
    Scanning... Station is 1380 AM
    Scanning... Station is 1510 AM
    Switching to FM
    Scanning... Station is 89.1 FM
    Scanning... Station is 103.9 FM
    Scanning... Station is 81.3 FM
    Scanning... Station is 89.1 FM
    Switching to AM
    Scanning... Station is 1250 AM
    Scanning... Station is 1380 AM
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```


### Strategy Method
* What is this pattern about?
Define a family of algorithms, encapsulate each one, and make them interchangeable.
Strategy lets the algorithm vary independently from clients that use it.

* TL;DR
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


def main():
    """
    >>> order = Order(100, discount_strategy=ten_percent_discount)
    >>> print(order)
    <Order price: 100 with discount strategy: ten_percent_discount>
    >>> print(order.apply_discount())
    90.0
    >>> order = Order(100, discount_strategy=on_sale_discount)
    >>> print(order)
    <Order price: 100 with discount strategy: on_sale_discount>
    >>> print(order.apply_discount())
    55.0
    >>> order = Order(10, discount_strategy=on_sale_discount)
    Discount cannot be applied due to negative price resulting. on_sale_discount
    >>> print(order)
    <Order price: 10 with discount strategy: None>
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Template Method
* Examples in Python ecosystem:
Django class based views: https://docs.djangoproject.com/en/2.1/topics/class-based-views/


* TL;DR
**Defines the skeleton of a base algorithm, deferring definition of exact
steps to subclasses.**

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


def main():
    """
    >>> template_function(get_text, to_save=True)
    Got `plain-text`
    Skip conversion
    [SAVE]
    `plain-text` was processed

    >>> template_function(get_pdf, converter=convert_to_text)
    Got `pdf`
    [CONVERT]
    `pdf as text` was processed

    >>> template_function(get_csv, to_save=True)
    Got `csv`
    Skip conversion
    [SAVE]
    `csv` was processed
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

### Visitor Method
* http://peter-hoffmann.com/2010/extrinsic-visitor-pattern-python-inheritance.html

* Examples in Python ecosystem:
  - Python's ast.NodeVisitor: https://github.com/python/cpython/blob/master/Lib/ast.py#L250
which is then being used e.g. in tools like `pyflakes`.
  - `Black` formatter tool implements it's own: https://github.com/ambv/black/blob/master/black.py#L718

* TL;DR
**Separates an algorithm from an object structure on which it operates.**

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


def main():
    """
    >>> a, b, c = A(), B(), C()
    >>> visitor = Visitor()

    >>> visitor.visit(a)
    generic_visit A

    >>> visitor.visit(b)
    visit_B B

    >>> visitor.visit(c)
    visit_B C
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod()
```

---

## Others

### Dependency Injection

"""
Dependency Injection (DI) is a technique whereby one object supplies the dependencies (services)
to another object (client).
It allows to decouple objects: no need to change client code simply because an object it depends on
needs to be changed to a different one. (Open/Closed principle)

In the following example `time_provider` (service) is embedded into TimeDisplay (client).
If such service performed an expensive operation you would like to substitute or mock it in tests.

```python
class TimeDisplay(object):

    def __init__(self):
        self.time_provider = datetime.datetime.now

    def get_current_time_as_html_fragment(self):
        current_time = self.time_provider()
        current_time_as_html_fragment = "<span class=\"tinyBoldText\">{}</span>".format(current_time)
        return current_time_as_html_fragment

```

```python
import datetime
from typing import Callable


class ConstructorInjection:
    def __init__(self, time_provider: Callable) -> None:
        self.time_provider = time_provider

    def get_current_time_as_html_fragment(self) -> str:
        current_time = self.time_provider()
        current_time_as_html_fragment = '<span class="tinyBoldText">{}</span>'.format(
            current_time
        )
        return current_time_as_html_fragment


class ParameterInjection:
    def __init__(self) -> None:
        pass

    def get_current_time_as_html_fragment(self, time_provider: Callable) -> str:
        current_time = time_provider()
        current_time_as_html_fragment = '<span class="tinyBoldText">{}</span>'.format(
            current_time
        )
        return current_time_as_html_fragment


class SetterInjection:
    """Setter Injection"""

    def __init__(self):
        pass

    def set_time_provider(self, time_provider: Callable):
        self.time_provider = time_provider

    def get_current_time_as_html_fragment(self):
        current_time = self.time_provider()
        current_time_as_html_fragment = '<span class="tinyBoldText">{}</span>'.format(
            current_time
        )
        return current_time_as_html_fragment


def production_code_time_provider() -> str:
    """
    Production code version of the time provider (just a wrapper for formatting
    datetime for this example).
    """
    current_time = datetime.datetime.now()
    current_time_formatted = f"{current_time.hour}:{current_time.minute}"
    return current_time_formatted


def midnight_time_provider() -> str:
    """Hard-coded stub"""
    return "24:01"


def main():
    """
    >>> time_with_ci1 = ConstructorInjection(midnight_time_provider)
    >>> time_with_ci1.get_current_time_as_html_fragment()
    '<span class="tinyBoldText">24:01</span>'

    >>> time_with_ci2 = ConstructorInjection(production_code_time_provider)
    >>> time_with_ci2.get_current_time_as_html_fragment()
    '<span class="tinyBoldText">...</span>'

    >>> time_with_pi = ParameterInjection()
    >>> time_with_pi.get_current_time_as_html_fragment(midnight_time_provider)
    '<span class="tinyBoldText">24:01</span>'

    >>> time_with_si = SetterInjection()

    >>> time_with_si.get_current_time_as_html_fragment()
    Traceback (most recent call last):
    ...
    AttributeError: 'SetterInjection' object has no attribute 'time_provider'

    >>> time_with_si.set_time_provider(midnight_time_provider)
    >>> time_with_si.get_current_time_as_html_fragment()
    '<span class="tinyBoldText">24:01</span>'
    """


if __name__ == "__main__":
    import doctest

    doctest.testmod(optionflags=doctest.ELLIPSIS)
```

---

### Page object

The page object pattern intends to create an object for each part of a web page. This technique helps build a separation between the test code and the actual code that interacts with the web page.

```python
from element import BasePageElement
from locators import MainPageLocators

class SearchTextElement(BasePageElement):
    """This class gets the search text from the specified locator"""

    #The locator for search box where search string is entered
    locator = 'q'


class BasePage(object):
    """Base class to initialize the base page that will be called from all
    pages"""

    def __init__(self, driver):
        self.driver = driver


class MainPage(BasePage):
    """Home page action methods come here. I.e. Python.org"""

    #Declares a variable that will contain the retrieved text
    search_text_element = SearchTextElement()

    def is_title_matches(self):
        """Verifies that the hardcoded text "Python" appears in page title"""

        return "Python" in self.driver.title

    def click_go_button(self):
        """Triggers the search"""

        element = self.driver.find_element(*MainPageLocators.GO_BUTTON)
        element.click()


class SearchResultsPage(BasePage):
    """Search results page action methods come here"""

    def is_results_found(self):
        # Probably should search for this text in the specific page
        # element, but as for now it works fine
        return "No results found." not in self.driver.page_source
```

---

## References
 - https://github.com/faif/python-patterns
 - https://selenium-python.readthedocs.io/page-objects.html
