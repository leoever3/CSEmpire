### Abstract

**To play a guiter song in java.**

* Packages
* Interface & Abstract classes
* Simple data structure
* Iteration & Exception

### Words

* Synthesizer 音箱合成器
* Redundancies  解雇

### Introduction

* A **package** is a **namespace** that organizes a set of related classes and interfaces.
  * Folders

* Abtract ---> concrete
* Interface -- abstract class -- class -- subclass

### Task

* Create a synthesizer package inteded for use by programs that want to simulate the sound of instruments

#### Task1

* An **interface** is a formal contract between a class and the outside world.
* If a class claims to implement an interface, then all methods defined by that interface must appear in the class.

#### Task2

* Methods and classes can be declared as abstract using the **abstract** keyword.
* **Abstract class** cannot be instantiated, but they can be subclassed using the **extends** keyword.
* Unlike interfaces, abstract classes can **provide implementation inheritance** for features other than public methods, including instance variables.

* Classes that implement interfaces will inherit all of the methods and variables from that interface. If an implementing class fails to implement any abstract methods inherited from an interface, then that class must be declared **abstract**.

##### Interfaces VS abstract classes

* Interface -- can do
* Abstract class -- "is-a"

#### Task3

* Implement the class
* throw exception

#### Task4

* Karplus-Algorithm

#### Task5

```java
public interface BoundedQueue<T> extends Iterable<T>
```

* last -- empty for enter
* First -- fill what we have to delete

```java
		public Iterator<T> iterator() {
        return new ArrayRingBufferIterator();
    }

    private class ArrayRingBufferIterator implements Iterator<T> {
        private int counter;

        ArrayRingBufferIterator() {
            counter = 0;
        }

        public boolean hasNext() {
            return counter < fillCount;
        }

        public T next() {
            int pos = first + counter;
            if (pos >= capacity) {
                pos = pos - capacity;
            }
            T returnItem = rb[pos];
            counter += 1;
            return returnItem;
        }
    }
```



### Issues

###### Interface declaration with generics

```java
public interface List61B<Item> {
  /**
   * Gets an item from the front.
   */
  public Item getFirst();

    /** Prints the list. Works for ANY kind of list. */
    default public void print() {
        for (int i = 0; i < size(); i = i + 1) {
            System.out.print(get(i) + " ");
        }
    }
}
```

###### Classes implement the interface with generics

```java
public class AList<Item> implements List61B<Item>
```

###### Generics Array

```java
rb = (T[]) new Object[capacity];
```

###### Default in interface

* Implement the method in the interface
  * Do things
* Why using default

This is for backwards compatibility.

If you have an interface that other people have implemented then if you add a new method to the interface all existing implementations are broken.

By adding a new method with a default implementation you remaining source-compatible with existing implementations.

###### Protect

* It means that only subclasses and classes in the same package can access this variable/field/

###### Double -- long --int

```java
int y = (int)Math.round(x);
```

###### Check Style

* Right click the .java file to find the check style

![Check Style Menu](https://sp18.datastructur.es/materials/guides/img/plugin-checkstyle-button.png)