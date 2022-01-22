### Search Problem

* When we use Data Structure
  * Given a stream of data, retrive information of interest.
  * To solve the search problem

### Abstract Data Types

* We define the **behavior** not the implementation.

| Name          | Store Operation(s)               | Primary Retrieval Operation | Retrieve By              |
| ------------- | -------------------------------- | --------------------------- | ------------------------ |
| List          | `add(key)`, `insert(key, index)` | `get(index)`                | index                    |
| Map           | `put(key, value)`                | `get(key)`                  | key identity             |
| Set           | `add(key)`                       | `containsKey(key)`          | key identity             |
| PQ            | `add(key)`                       | `getSmallest()`             | key order (aka key size) |
| Disjoint Sets | `connect(int1, int2)`            | `isConnected(int1, int2)`   | two integer values       |

### Implementation

![image-20220108153855980](/Users/morningstar/Library/Application Support/typora-user-images/image-20220108153855980.png)

### Abstraction

* Abstraction often happens in **layers**.
* In Priority Queue ADT
  * Heap ordered tree + 5 approaches(1A, 1B, 1C, 2, 3) of representing a tree

* In External Chaining Hash Table
  * Array of buckets + buckets can be done using array list, BST ...

![image-20220108154051966](/Users/morningstar/Library/Application Support/typora-user-images/image-20220108154051966.png)

### Wiki

![img](https://lh6.googleusercontent.com/asJRfTW3MC7xxwqC8YLFgtCHzgUuhL9yETJir75rIZeC1wf7rISxlTVseiYmkMoaM4uq9-8IIniQJ6P5hiqVDGtWZVxjVPmHsZ2TMaAgzyzKB_tipFymmNWVE8nt9ASgikH2Cq-THYM)