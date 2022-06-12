## Object-Oriented Programming

**Object-oriented programming** (OOP) is a style of programming that allows you to think of code in terms of "objects." Here's an example of a `Car` class:

```python
class Car:
    num_wheels = 4

    def __init__(self, color):
        self.wheels = Car.num_wheels
        self.color = color

    def drive(self):
        if self.wheels <= Car.num_wheels:
            return self.color + ' car cannot drive!'
        return self.color + ' car goes vroom!'

    def pop_tire(self):
        if self.wheels > 0:
            self.wheels -= 1
```

Here's some terminology:

- **class**: a blueprint for how to build a certain type of object. The `Car` class (shown above) describes the behavior and data that all `Car` objects have.

- **instance**: a particular occurrence of a class. In Python, we create instances of a class like this:

  ```python
  >>> my_car = Car('red')
  ```

  `my_car` is an instance of the `Car` class.

- **data attributes**: a variable that belongs to the instance (also called instance variables). Think of a data attribute as a quality of the object: cars have *wheels* and *color*, so we have given our `Car` instance `self.wheels` and `self.color` attributes. We can access attributes using **dot notation**:

  ```python
  >>> my_car.color
  'red'
  >>> my_car.wheels
  4
  ```

- **method**: Methods are just like normal functions, except that they are bound to an instance. Think of a method as a "verb" of the class: cars can *drive* and also *pop their tires*, so we have given our `Car` instance the methods `drive` and `pop_tire`. We call methods using **dot notation**:

  ```python
  >>> my_car = Car('red')
  >>> my_car.drive()
  'red car goes vroom!'
  ```

- **constructor**: As with data abstraction, constructors build an instance of the class. The constructor for car objects is `Car(color)`. When Python calls that constructor, it immediately calls the `__init__` method. That's where we initialize the data attributes:

  ```python
  def __init__(self, color):
      self.wheels = Car.num_wheels
      self.color = color
  ```

  The constructor takes in one argument, `color`. As you can see, this constructor also creates the `self.wheels` and `self.color` attributes.

- `self`: in Python, `self` is the first parameter for many methods (in this class, we will only use methods whose first parameter is `self`). When a method is called, `self` is bound to an instance of the class. For example:

  ```python
  >>> my_car = Car('red')
  >>> car.drive()
  ```

  Notice that the `drive` method takes in `self` as an argument, but it looks like we didn't pass one in! This is because the dot notation *implicitly* passes in `car` as `self` for us.