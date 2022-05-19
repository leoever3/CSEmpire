### IntList

* We defined `IntList` class **recursively**.
  * Lists of integers that can **change size**.
  * Writing a `size` **helper method**.
* But `IntList` are **Naked Data Structure**.
  * The programmer must utilize recursion for simple tasks.



### SLList

1. Rebranding
   * Turn `IntList` into `IntNode`
2. Bureaucracy
   * Create a new class called SingleLinked list
   * `addFirst`
   * `getFirst`
   * `addLast`
     * **Recursive Helper Methods**
3. Public vs. Private
4. **Nested Classes**
5. **Caching**
   * cache the size of list as an instance variable
6. **Sentinel Nodes**
   * Deal with Empty List
   * **Invariant**
     * Sentinel is always the first element in our list.

##### Codes

```java
/** An SLList is a list of integers, which hides the terrible truth
   * of the nakedness within. */
public class SLList {	
  
	private static class IntNode {
		public int item;
		public IntNode next;

		public IntNode(int i, IntNode n) {
			item = i;
			next = n;
			System.out.println(size);
		}
	} 

	/* The first item (if it exists) is at sentinel.next. */
	private IntNode sentinel;
	private int size;

	/** Creates an empty SLList. */
	public SLList() {
		sentinel = new IntNode(63, null);
		size = 0;
	}

	public SLList(int x) {
		sentinel = new IntNode(63, null);
		sentinel.next = new IntNode(x, null);
		size = 1;
	}

 	/** Adds x to the front of the list. */
 	public void addFirst(int x) {
 		sentinel.next = new IntNode(x, sentinel.next);
 		size = size + 1;
 	}

 	/** Returns the first item in the list. */
 	public int getFirst() {
 		return sentinel.next.item;
 	}

 	/** Adds x to the end of the list. */
 	public void addLast(int x) {
 		size = size + 1; 		
 		IntNode p = sentinel;
    
 		/* Advance p to the end of the list. */
 		while (p.next != null) {
 			p = p.next;
 		}
 		p.next = new IntNode(x, null);
 	}
 	
 	/** Returns the size of the list. */
 	public int size() {
 		return size;
 	}

	public static void main(String[] args) {
 		/* Creates a list of one integer, namely 10 */
 		SLList L = new SLList();
 		L.addLast(20);
 		System.out.println(L.size());
 	}
}
```



### DLList

7. Looking Back -- two pointer

   1. `next`
   2. `prev`

8. Sentinel Upgrade

9. **Generic**

   * ```java
     DLList<String> list = new DLList<>("bone");
     ```



### AList

#### Array

* Boxes of bits
* Instantiating Arrays
  * `int[] y = new int[3];`
  * `int[] x = new int[]{1, 2, 3, 4, 5};`
* `Arraycopy`

* 2D Arrays
  * `int[][] array = new int[4][];`

#### ArrayList - resizing

* Improve the **speed** of getting the i'th item

* Resizing
  * `size * FACTOR`

##### Codes

Golden point: **Inserts item into given position.**

```java
/** Array based list.
 *  @author Josh Hug
 */

/* The next item ALWAYS goes in the size position */

public class AList<Item> implements List61B<Item>{
	/* the stored integers */
	private Item[] items;
	private int size;

	private static int RFACTOR = 2;

    /** Creates an empty list. */
    public AList() {
    	size = 0;
    	items = (Item[]) new Object[100];
    }

    /** Resize our backing array so that it is
      * of the given capacity. */
    private void resize(int capacity) {
    	Item[] a = (Item[]) new Object[capacity];
    	System.arraycopy(items, 0, a, 0, size);
    	items = a;    	
    }

    @Override
    /** Inserts X into the back of the list. */
    public void addLast(Item x) {
    	if (size == items.length) {
    		resize(size * RFACTOR);
    	}

    	items[size] = x;
    	size = size + 1;
    }

    @Override
    /** Returns the item from the back of the list. */
    public Item getLast() {
    	int lastActualItemIndex = size - 1;
    	return items[lastActualItemIndex];
    }

    @Override
    /** Gets the ith item in the list (0 is the front). */
    public Item get(int i) {
        return items[i];
    }

    @Override
    /** Returns the number of items in the list. */
    public int size() {
        return size;        
    }

    @Override
    /** Deletes item from back of the list and
      * returns deleted item. */
    public Item removeLast() {
		Item itemToReturn = getLast();
		/* setting to zero not strictly necessary, but
		 * it's a good habit (we'll see why soon) */
		items[size - 1] = null;
		size = size - 1;
		return itemToReturn;
    }

    @Override
    /** Inserts item into given position.
      * Code from discussion #3 */
    public void insert(Item x, int position) {
        Item[] newItems = (Item[]) new Object[items.length + 1];

        System.arraycopy(items, 0, newItems, 0, position);
        newItems[position] = x;

        System.arraycopy(items, position, newItems, position + 1, items.length - position);
        items = newItems;
    }

    @Override
    /** Inserts an item at the front. */
    public void addFirst(Item x) {
        insert(x, 0);
    }

    @Override
    /** Gets an item from the front. */
    public Item getFirst() {
        return get(0);
    }
}
```

