### Asymptotics

* To **evaluate the performance** of programs using math
* **Time complexity**
* Only valid on very **large inputs**

|       | Bound          |                                                           |
| ----- | -------------- | --------------------------------------------------------- |
| Big O | Upper bound    | Worst case                                                |
| Big Ω | Lower bound    | Best case                                                 |
| Big Θ | Tightest bound | **Exist** when tightest worst case = tightest lower bound |

##### Iteration Asymptotics -- 2 Sum

* 1 + 2 + 3 + . . . + N = Θ(N^2)
* 1 + 2 + 4 + . . . + N = Θ(N)

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



### Heaps



### Graphs

|                                        | Name                       | Description                                                | ADT                       | Other's                          |
| -------------------------------------- | -------------------------- | ---------------------------------------------------------- | ------------------------- | -------------------------------- |
| **Traversal**                          | DFS (Depth First Search)   | We visit each subtree in some order the end of the tree.   | **Recursion** / Stack     | Pre-order/In-order/Post-order    |
|                                        | BFS (Breadth First Search) | We visit the nodes level by level.                         | **Queue** (FIFO)          | DisTo[]                          |
| **Shortest Paths** (Edges have weight) | Dijkstra's                 | Find the shortest paths from node to **every other node**  | **Priority Queue** (Heap) |                                  |
|                                        | A*                         | Find the shortest path from source to the **target**       | **Priority Queue** (Heap) | Priority = DisTo[] + Heuristic() |
| Minimum Spanning Trees (**MST**)       | Prim's                     | Have a start node, add the lightest edge that is unvisited |                           |                                  |
|                                        | Kruskal's                  | Adding the lightest edge if does not cause a cycle         | **Disjoint Set**          | Sorting all the edges            |

