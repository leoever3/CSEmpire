### Plugin

CS61B Plugin

**Check Style**

##### Java Visualizer



### Junit

[JUnit](http://junit.org/) is a Unit Testing Framework for Java.



```java
import static org.junit.Assert.*;
import org.junit.Test;
```

When you create JUnit test files, you should precede each test method with a `@Test` annotation

**All tests must be non-static.**

red/green arrows **default redered**

white/blue boxes **jh61b renderer**

```java
at ArithmeticTest.testSum(ArithmeticTest.java:25)
```

Test-Driven Development (TDD) cycle

Timeout:

```java
@Test(timeout = 1000)
```

“red” phase

```java
public static IntList reverse(IntList A) {
        IntList reversed = null;
        IntList remember = null;
        while (A != null) {
            remember = A.rest;
            A.rest = reversed;
            reversed = A;
            A = remember;
        }
        A = reversed;
        return A;
//        if (A == null) {
//            return null;
//        }
//        IntList B = null;
//        while (A != null) {
//            B = new IntList(A.first, B);
//            A = A.rest;
//        }
//        return B;
    }
```

## A Debugging Mystery

Integer is no bigger than 128.