### Comparison Sorts

###### Stability

* Two elements that are the equal are ordered the same in final result as in original list

###### Inversion

* an out of place pair



#### Selection Sort

* Move minimum of unsorted to the left

###### Runtime:

1 + 2 + 3 + .. + N = **Θ(N^2)**

* Best case: Θ(N^2)

* Worst case: Θ(N^2)

###### Why use?

* Simple to code
* Minimize swapping operations -- only N swaps
* Pretty bad overall though

###### Stable?

* **No**
* Because we swap tje element

[2a 2b 1] --> [1 2b 2a] -- > [1 2b 2a]



#### HeapSort:

1. Bottom up heapification to **build a maxheap**
   * bubble down everyone from the end

2. Repeat N times:
   * **removeMax** and put max at end
   * **Bubble down** to create smaller maxheap while growing sorted array from righthand side of array

###### Bottomup

**Original array** ----bottom up heapification (Θ(N)) ----> **MaxHeapArray** ----Iterative process of removeMax (placing Max at end) ----> **Sorted Array**



###### Why using maxheap?

* When we removeMax, we remove the top of the heap and put it in the end of array.
* At the same time, we need to put the last item in the heap to the front which is the position the Max should go to.
* So it is good that, we just **swap the Max and the last** and then to bubble down to create the new smaller heap, we finish our job.

###### Runtime:

1. Heapifying the array -- **Θ(N)**
2. Bubble down operation -- Θ(N log N)

* Best case: Θ(N) -- all the elements are duplicate
* Worst case: **Θ(N log N)**

###### Why use?

* Good worst case bound
* If we already are given a heap
* In-place -- constant space complexity



#### Insersion Sort

* For each element, keep swapping it to the left until it's bigger than the left element
* Build sorted sublist on left side of list

###### Runtime:

* Best case: **Θ(N)** -- input list sorted ascending
* Worst case: **Θ(N^2)** -- input list sorted descending

**Θ(N + K)**

* N looking at each element
* Total swaps that we do!

###### Why use?

* Very fast on **small inputs** (n < 15)
* Very fast when the input list is **nearly sorted**



#### MergeSort

* Kepp merging runs together, starting with runs of size zero / one

###### Pseudocode

```java
function mergesort(list)
	if (list is of length 0 or 1)
		return list;
	a = mergesort(left half of list)
	b = mergesort(right half of list)
	return merge(a, b)
```

###### Runtime:

* Best case: **Θ(N log N)**
* Worst case: **Θ(N log N)**

###### Why use?

* good worst case bound

* Stable -- often used with objects
* good with linked lists



### Quicksort

#### 3 Scan:

1. Choose a pivot and partition into 3 groups

* Smaller than pivot
* equal
* greater than pivot

2. Recurse on each group

##### Hoare Partitioning

1. Let first item be pivot
2. Create two points **L** and **G**
   1. L likes smaller / equal elements start at **left**
   2. G likes larger elements start at **right**
3. Move pointers, stop on disliked items
4. If both stopped, **swap** L and G and move pointers

5. Done when pointers cross, then swap G & pivot

###### Why use?

* The fastest sort
* In place with Haore
* Stable with 3-scan

###### Runtime:

* Best case: **Θ(N log N)**
* Worst case: **Θ(N^2)**





### Radix Sorts

* A **radix** can be thought of as the alphabet or set of digits to choose form in some system.
  * The **radix size** of the English alphabat is 26.
  * The **radix size** of the Arabic numerals is 10.
* We use **counting sorts** to sorts each **digit**.

#### LSD Radix Sort

* Repeatedly sort the same list on each digit, going from the least significant digit to the most significant digit.

###### Why works?

A = 1200, B = 1210

* Notice that A and B first differ at second least significant spot.
* After we sort all the numbers on that digit, A will be before B.
* Since every later pass is **stable**, A will remain before B.

#### MSD Radix Sort

* Sort fro the most significant digit to the least significant digit
* Recurse on each **subgroup** comparing next digit



How can we leverage the fact that each digit is in a **finite range 0 - 9**?

#### Counting Sort

* Create an array of length 10, since there are 10 digits (Radix) -- Θ(R)
* Count number of items at each digit. -- Θ(N)
* Find starting points for each digit. -- Θ(R)
* Put in final array. -- Θ(N)

###### Runtime:

* **Θ(R + N)**

###### LSD Runtime

* **Θ(W(R + N))**
* W -- width of the numbers

###### MSD Runtime

* Best case: **Θ(R + N)**
* Worst case: **Θ(W(R + N)**



### Searching & Sorting

![image-20220205202533307](/Users/morningstar/Library/Application Support/typora-user-images/image-20220205202533307.png)