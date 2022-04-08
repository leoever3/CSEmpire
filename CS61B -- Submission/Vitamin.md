##### Java Syntax

In Java, all code lives inside a **class**.

##### Variables

Variables have declared types, also called their **static** type.

##### Variable Types

There are two types of variables in Java: **references** and **primitive**

##### GRoE

According to the Golden Rule of Equals, given variables x and y, when we say y = x, we are **copy** the bits from x into y.

##### Access

We use the **private** keyword to prevent other classes from using members (or constructors) of a class.



##### List

We use a **sentinel** node to allow the representation of the empty DLList.

##### ArrayLists

If we add an element to an array list and there is no space in the underlying array, then we must **resize** the array in order to make room

##### Junit

org.junit.Assert.assertEquals(expected, actual) will test that expected is **equal** to actual and fails if this is not true

If we want JUnit to identify a method to be run in a testing suite, we can annotate the method with **@org.junit.test**

##### Method Variety

When we have multiple methods with the same name but different parameters, we call this method **overloading**.



##### Inheritance

The technique of completely hiding the implementation of a module is called **encapsulation**.

##### CompareTo

**Comparable** is the interface that a class must implement to allow comparisons with itself and other objects?

##### Autoboxing

An example of autoboxing is when Java automatically turns an int into an **integer**.

##### Generics

When you use the “extends” keyword in a generic method, we call this **type** upper bounding.

##### Exception

Unlike subclasses of RuntimeException and Error, all other Throwables are **checked**.

##### Iterators

To support the enhanced for loop, a class must implement the **iterable** interface.



##### Packages

A package is a **namespace** that organizes classes and interfaces.

##### Modifier Keywords

The four access modifier keyworks are private, package-private, **protected** and public.

##### Equals

The equals method always takes in a(n) **static** instance.

##### Class Design

**Extension** is a design practice when we have a private instance of a class we want to add functionality to, and use its methods to create new functionality.



##### Graphs

A graph is a set of vertices connected by **edges.**

A graph can be directed or **undirected**.

The three most common ways of representing graphs are through lists of edges, adjacency lists, and adjacency **matrix.**

##### Shortest Paths

When we have a single target in mind for shortest paths, we would usually rather use **A*** over Dijkstra's algorithm.

Kruskal's algorithm finds a **MST** of a graph.

n the A* algorithm, a heuristic which overestimates is **trueDistance.**



##### Sorting

Given a sublinear number of inversions on a list, **insertion sort** has the fastest runtime.

Quick sort (on a list of n*n* items) in the average case has a runtime of Θ(**nlogn**)

Merge sort (on a list of n*n* items) in the worst case has a runtime of Θ(**nlogn**)

If the relative order of equivalent items is kept the same, the sort is said to be **stable.**

In the very best case, given an input of size N and an alphabet of size K, MSD sorting has a runtime of Θ (N + R)

##### Tries

Tries are analogous to **radix** sort. [note for those of you who have this one before: the answer for this problem has changed]

Typically in a trie, letters are stored implicitly on (nodes or **edges**?) 



##### Compression

When we represent symbols as code words, we can avoid ambiguity by making the words **prefix** free.

To decode a file compressed with Huffman encoding, we need to look up longest matching prefix. The data structure that we use to do this is a **trie**.

##### NP-Completeness

A problem is NP-complete if it is a member of NP and it **reduces** every other problem in NP.

Independent set cracks 3-SAT. This is done by creating an instance G of the independent set input S where, for each clause in S, we create 3 vertices in a triangle and add an edge between each literal and its **negation**. We can then run independent set and the result will be a solution for 3-SAT.



##### Git

The **git checkout** command is used to restore your files in git to an earlier state.

##### Debugging

A **conditional breakpoint** is a special type of IntelliJ breakpoint that only stops under certain conditions.

Changing an object that is inside a hash or tree based data structure can cause problems. We can avoid these by making the class for that object **immutable**.

Writing your own unit tests in the real world is extremely important, but students seem to prefer using the **autograder**.