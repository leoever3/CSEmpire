### Hello Java

#### Class

* All code lives inside a **class**.
* The code that is executed is inside a **function** (method).
* **{}** are used to denote the beginning and end of a section of code.
* Statements end with **;**
* Variables have declared types. -- **static type**

#### Static Typing

* Types are checked before the program is even run.
  * **Compile time**



### Classes

#### Main Methods

* A java program without a main method cannot be run directly.
* `public static void main(String[] args)`
  * `public`: access
  * `static`: not associated with any particular instance
  * `void`: no return type
  * `main`: name of the method
  * `String[] args`:
    * a **parameter** that is passed to the main method
    * command line arguments

#### Class Declaration

* Members of the class
  * Methods
  * Variables
* We access members of a claas using **dot** notation

##### Constructors

* Constructors tell Java what to do when a program tries to create an instance of a class.

#### Class Instantiation

* `new`
* An instance of a class in Java is also called an **Object**
* Array instantiation
  * `int[] arr = new int[10]`

#### Static vs. Instance methods /variables

* **Instance** methods are actions that can only be taken by an instance of the class
  * `d.bark()`
* **Static** methods are taken by the class itself.
  * `Math.sqrt()`

#### Command Line Arguments

* Arguments can be provided by the operating system to the program as "**command line arguments**"
* `java Hello Josh`



### Reference

#### Bits

* The computer stores information as memory, and represents this information using sequences if bits -- **either 0 or 1.**

#### Primitives Types

* Primitives are representations of **information**.
* 8 primitive types
  * **byte, short, int, long, float, double, boolean, char**
  * ints are 32 bits, bytes are 8 bits.
* Declaring Primitives
  * `int x;`
  * We set aside enouthg memory space (32 bits) to hold the bits.

#### Reference Types

##### Creating objects

* When we create an instance of a class using `new` keyword, Java creates **boxes** of bits for each field.
* The constructor comes in and fills in these bits to their approriate values.
* The return value of the constructor will return the **location in memory** where the boxes live (usually 64 bits)
* This address can then be stored in a variable with a **reference type**.

##### Reference Types

* If a variable is not a primitive type then it is a reference type.
* **64 bits**
* The variable does not store the entire object itself.

#### Golden Rule of Equals

* When we assign a value with equals, **we are just copying the bits from one memory box to another.**
  * primitive -- copies the actual value
  * reference types -- do the same thing but copy the address
* **Parameter Passing**
  * `average(double a, double b)`
  * we copy the **bits** form those variables into the parameter variables.

#### Array

* **Arrays** are also Objects.
* `int[] arr = new int[]{0, 1, 2, 3, 4};`
* `x` stores the location of this array
* The **size** of the array was specified when the array was created and cannot be changed.



### Testing

#### TDD

* **Test-Driven Development**
  * The programmer writes the tests for a function **before** the actual function is written.

#### Junit Tests

* A package that is used to debug programs in Java
  * `assertEquals(expected, actual)`



### Autoboxing

| Primitive | Class     |
| --------- | --------- |
| byte      | Byte      |
| short     | Short     |
| int       | Integer   |
| long      | Long      |
| float     | Float     |
| double    | Double    |
| boolean   | Boolean   |
| Char      | Character |



### Immutability

* An immutable data type is a data type whose instances cannot change in any observable way after instantiation.
  * String
  * `final`



### Generic

* Specification of generic types for methods (before return type).

```java
public static <K,V> V get(Map61B<K,V> map, K key) {
    if map.containsKey(key) {
        return map.get(key);
    }
    return null;
}
```

