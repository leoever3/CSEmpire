### Abstract

**Using built in Disjoint set (UF) to simulate percolation (from bottom to top)**

* **Disjoint Sets** -- built-in -- Princeton library
  * void **union**(int p, int q): Unions two items.
  * boolean **connected**(int p, int q): Returns true if items are connected.
  * int **find**(int p): Returns set number of a given item.
* To solve **dynamic connected** problem
* utilize existing data structure 

###### Create 2 classes

* **Percolation** -- simulate percolation problem
  * We have a path from the top to the bottom
  * Porosity 孔隙率
  * Elucidate: make something clear 
  * cascading errors 小瀑布
* **PercolationStats** -- do experiments with percolation
  * To estimate the percolation **threshold**
  * Given a porous landscape with water on the surface (or oil below), under what conditions will the water be able to **drain through to the bottom** (or the oil to gush through to the surface)?
  * p: 0.593



Translate from UF to Percolation

* Two-dimension Array?

* Mapping from 2-dimensional to 1 dimensional -- unique number? 

  * private help method to generate a unique number

  * ```java 
    private int xyTo1d (int x, int y)
    ```

* isfull
  * Virtual grid union all the top
  * Union(9999, x) make the runtime from linear to constant 

* How to solve backwash?



### Issues

###### Passing in command line arguments in itellij

* Run -- edit configuration -- program arguments

###### Backwash

* **Build 2 Unconfined sets** 
  * One for isFull() -- not union the bottom together to avoid backwash
  * Another for percolation() -- union both the top and the bottom to have constant runtime.