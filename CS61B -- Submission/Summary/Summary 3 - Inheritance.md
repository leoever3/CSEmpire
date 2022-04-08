### Inheritance

#### Classes

* **Subclasses** are classes that extend another class.
  * They have access to all of the functions and variables of their parent class in addition to any functions and variables defined in the child class.
* **Superclasses** are classes that are extended by another class.
* Classes can only extend **one** class but can be extended by many classes.
* `extends`
* `super()`
  * Call to its super class

* abstract class

#### Interfaces

* **Interfaces** are **implemented** by classes. They describe a narrow ability that can apply to many classes that may or may not be related to one another.
* Interfaces are like **abstract classes** in that they do not usually implement the methods they specify.
* One class can implement **many** interfaces.
* `implements`
* `class Pitbull extends Dog implments Squishable, Photogenic{}`
* **Default Methods**
  * Interfaces can have default methods


#### Overloading vs. Overriding

* **Method Overloading** is done when ther are multiple methods with the smae name and return tyoe, but different parameters.
* **Method Overriding** is done when a **subclass** has a method with the exact same function signature as a method in its superclass.

#### Casting

* **Casting** allows our compiler to overlook cases where we are calling a method that belongs to a subclass on a variable that is statically typed to be the super class.
  * `Animal a = new Dog();`
  * `Dog d = (Dog) a;`


#### Dynamic Method Selection

* **Static Type vs. Dynamic Type**
  * `Animal s = new Dog();`

* Compile Time
  * Check for valid variable assignments
  * Check for valid method calls (onlu considering static type and static superclasses)
* Run Time
  * Check for overridden methods
  * Ensure casted objects can be assigned to their variables





### Subtype Polymorphism

* Subtype Polymorphism allows us to use a subtype of a class or interface **in its place** so we can write functions that can operate on a wide array of objects so long as they have a certain **attribute in common**.

```java
class Dog extends Animal{}
Animal d = new Dog();
class Cat extends Animal{}
Animal c = new Cat();
d.compareTo(c);
```



### Comparable

* **`Comparable<>` interface**
* **compareTo** method

```java
public class Dog implements Comparable<Dog> {
    ...
    public int compareTo(Dog uddaDog) {
        return this.size - uddaDog.size;
    }

    private static class NameComparator implements Comparator<Dog> {
        public int compare(Dog a, Dog b) {
            return a.name.compareTo(b.name);
        }
    }

    public static Comparator<Dog> getNameComparator() {
        return new NameComparator();
    }
}
```



### Exceptions

* **Exceptions** are used to stop the code and inform the person running it when something occurs that is not allowed.
  * NullPointerException
  * IndexOutOfBoundsException
* `throw new RuntimeException("Because I said so.")`
* Try - catch



### Iterators & Iterable

* Iterators are objects that can be iterated through in Java (enhanced loop)

```java
public interface Iterator<T> {
		boolean hasNext();
		T next();
}
```

* Iterables are objects that can **produce an iterator**.

```java
public interface Iterable<T> {
  	Iterator<T> iterator();
}
```
