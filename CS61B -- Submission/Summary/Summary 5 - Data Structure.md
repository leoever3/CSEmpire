### Asymptotics

* To **evaluate the performance** of programs using math
* **Time complexity**
* Only valid on very **large inputs**

|       | Bound          |                                                           |
| ----- | -------------- | --------------------------------------------------------- |
| Big O | Upper bound    | Worst case                                                |
| Big Ω | Lower bound    | Best case                                                 |
| Big Θ | Tightest bound | **Exist** when tightest worst case = tightest lower bound |

##### Iteration Asymptotics

* 2 Sum

  * 1 + 2 + 3 + . . . + N = Θ(N^2)

  * 1 + 2 + 4 + 8 + 16 . . . + N = Θ(N)


##### Recursion Asymptotic

1. Draw out the recuisive tree
   * A node for every function call
2. Determine **work per level**
3. Recognize **which sum** we are dealing with
4. Calculate the **height** of the tree



### ADTs

* **Abstract Data Type**
  * data structures where we know **what** they do but not how
* **Interfaces** or **abstract classes** in java

##### ADT VS. Implement

| ADTs           | List       | Map     | Set     | Priority Queue | Disjoint Set |
| -------------- | ---------- | ------- | ------- | -------------- | ------------ |
| **Implements** | ArrayList  | HashMap | HashSet | Heap           | QuickFind    |
|                | LinkedList | TreeMap | TreeSet |                | QuickUnion   |
|                |            |         |         |                | Weighted QU  |
|                |            |         |         |                | WQUPC        |



### Search Problem

* Given a stream of data, retrive information of interest.

##### ADT's behavior

| Name          | Store Operation(s)               | Primary Retrieval Operation | Retrieve By              |
| ------------- | -------------------------------- | --------------------------- | ------------------------ |
| List          | `add(key)`, `insert(key, index)` | `get(index)`                | index                    |
| Map           | `put(key, value)`                | `get(key)`                  | key identity             |
| Set           | `add(key)`                       | `containsKey(key)`          | key identity             |
| PQ            | `add(key)`                       | `getSmallest()`             | key order (aka key size) |
| Disjoint Sets | `connect(int1, int2)`            | `isConnected(int1, int2)`   | two integer values       |



### Disjoint Set

* Disjoint Sets also know as **Union Find** (UF)

```Java
public interface DisjointSet {
	void connect (x, y); // Connects nodes x and y (you may also see union)
	boolean isConnected(x, y); // Returns true if x and y are connected
}
```

#### Implements

| Implementation             | How to store                             | Constructor | `isConnected` | `connect` |
| -------------------------- | ---------------------------------------- | ----------- | ------------- | --------- |
| Quick Find                 | Array of integers                        | Θ(N)        | Θ(N)          | Θ(1)      |
| Quick Union                | **parent** of each node                  | Θ(N)        | O(N)          | O(N)      |
| Weighted Quick Union (WQU) | Merged by **size**                       | Θ(N)        | O(log N)      | O(log N)  |
| WQU with Path Compression  | **set’s root** whenever find() is called | Θ(N)        | O(α(N))*      | O(α(N))*  |



### Hashing

* **Hashing functions**
  * functions that represent an object using an integer.
* **Hash code**
  * We use the **hash code** to figure out which **bucket** of our hashes the item should go in.
  * **Module %**
* **Good hash code**
  * Distribute items **evenly**
* **Hash Table**
  * Final Data structure
  * Inputs are converted by a hash function into an integer -- Hashcode
  * Hashcodes are converted to a valid index using %
* In each **bucket**, we deal with having lots of item by **chaining** the items and using .equals to find what we are looking for.
* **Resize** the buckets -- load factor threshold



### Trees

#### Binary Search Trees

* Binary Search Trees are data structures that allow us to **quickly access elements in sorted order**.
* Properties
  * Each node in a BST is a **root** of a smaller BST
  * Each node to the **left** of a root has a value **lesser** than that of the root
  * Each node to the **right** of a root has a value **greater** than that of the root

* BSTS can be **bushy** or **spindly**

![image-20220109161150376](/Users/morningstar/Library/Application Support/typora-user-images/image-20220109161150376.png)

#### B-trees

* B-trees also refered to as **2-3 trees**.
* B-trees are trees that serve a similar function to binary tree while ensuring a **bushy structure**.
  * Not adding new leaves, instead **overstuff** the current leaf nodes
  * **Push** the middle element if the node is too big
* **Perfectly balanced but hard to implement**

![image-20220103124606768](/Users/morningstar/Library/Application Support/typora-user-images/image-20220103124606768.png)

* Each node can habe up to **2 items** and **3 children**.
* All leaves are the **same distance** from the root which makes getting take **Θ(log N)** time.

* There are variations known as **2-3-4 trees**.

#### Left Leaning Red Black Trees

* LLRBS are a representation of B-trees that we use beacause it is easy to work with in code.
  * Bijection with B-trees
  * Makeing the code **simple**
* Each multi-node in a 2-3 tree is represented using a **red** connection on the **left** side.

![image-20220103125412582](/Users/morningstar/Library/Application Support/typora-user-images/image-20220103125412582.png)

* **3 Balancing Operations**
  * RotateLeft(A)
    * Right leaning
  * RotateRight(A)
    * Overstuffed
  * ColorFlip(a)
    * Overstuffed
* Check
  * Still BST
  * All leaves shold be the same height
  * **Red links do not add the height**



### Heaps

* New ADT: **Priority Queue**

```java
/** (Min) Priority Queue: Allowing tracking and removal of 
  * the smallest item in a priority queue. */
public interface MinPQ<Item> {
    /** Adds the item to the priority queue. */
    public void add(Item x);
    /** Returns the smallest item in the priority queue. */
    public Item getSmallest();
    /** Removes the smallest item from the priority queue. */
    public Item removeSmallest();
    /** Returns the size of the priority queue. */
    public int size();
}
```

* Heaps are special trees that follow a few basic rules:

  * Heaps are **complete**
    * The oly empty parts of a heap are in the **botom** row, to the **right**

  * In a min-heap, each node must be smaller than all of its child nodes. The opposite is true for max-heaps.

* `swim()`
* Because the tree is complete, we can build **Array-based heaps** to save more space.



### Graphs

|                                        | Name                       | Description                                                | ADT                       | Other's                          |
| -------------------------------------- | -------------------------- | ---------------------------------------------------------- | ------------------------- | -------------------------------- |
| **Traversal**                          | DFS (Depth First Search)   | We visit each subtree in some order the end of the tree.   | **Recursion** / Stack     | Pre-order/In-order/Post-order    |
|                                        | BFS (Breadth First Search) | We visit the nodes level by level.                         | **Queue** (FIFO)          | DisTo[]                          |
| **Shortest Paths** (Edges have weight) | Dijkstra's                 | Find the shortest paths from node to **every other node**  | **Priority Queue** (Heap) |                                  |
|                                        | A*                         | Find the shortest path from source to the **target**       | **Priority Queue** (Heap) | Priority = DisTo[] + Heuristic() |
| Minimum Spanning Trees (**MST**)       | Prim's                     | Have a start node, add the lightest edge that is unvisited |                           |                                  |
|                                        | Kruskal's                  | Adding the lightest edge if does not cause a cycle         | **Disjoint Set**          | Sorting all the edges            |



### Tries

* Tries are special trees mostly used for language tasks.
* Each node in a trie is marked as being a word-end or not, so you can quickly check whether a word exists within your structure.

![image-20220115154857775](/Users/morningstar/Library/Application Support/typora-user-images/image-20220115154857775.png)



### Multiple Dimension Data

* **Uniform Partitioning**
  * Partition space into uniform chunks.
* **Quadtree**
  * Generalized 2D BST where each node “owns” 4 subspaces.
* **K-d tree**
  * Generalized k-d BST where each node “owns” 2 subspaces.
  * **Dimension** of ownership **cycles** with each level of depth in tree.
