### Abstract

* Making a **priority queue** using abinary **min-heap**
  * Min-heap: smaller values corrspond to higher priorities

Representing a tree with an array

* Sequence data structure
  * array
  * Linked nodes
    * BST

* Heaps:
  * Use an arry to represent a conplete tree

##### Complete binary tree

* The root of the tree wil be in position 1 of the array. (nothing is at position 0)
* The left child of a node at position n is at position **2n**
* The right child of a node at position n is at position **2n + 1**
* The parent of a node at position n is at position **n/2** (Round)



### Binary min-Heaps

* Binary trees
* The tree must be **complete**
* Every node is smaller than its descendants
  * This helps us access the min element quickly -- priority queue

###### Add an item

###### Remove the min item

#### Method

- leftIndex
- rightIndex
- parentIndex
- swim
- sink