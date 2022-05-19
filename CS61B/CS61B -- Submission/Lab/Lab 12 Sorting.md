### Abstraction

Mergesort and Quicksort on Linkedlist





##### Merge Sort on LinkedLists

* Using iteration
* Quene of Queue of Item

```java
public static <Item extends Comparable> Queue<Item> mergeSort(
            Queue<Item> items) {
        // Your code here!
        if (items.size() <= 1) {
            return items;
        }
        Queue<Queue<Item>> qqi = makeSingleItemQueues(items);
        while (qqi.size() > 1) {
            Queue<Queue<Item>> temp = new Queue<>();
            while (!qqi.isEmpty()) {
                if (qqi.size() == 1) {
                    temp.enqueue(qqi.dequeue());
                } else {
                    temp.enqueue(mergeSortedQueues(qqi.dequeue(), qqi.dequeue()));
                }
            }
            qqi = temp;
        }
        items = qqi.dequeue();
        return items;
    }
```



##### Quick Sort on LinkedLists

* Using recursion

```java
public static <Item extends Comparable> Queue<Item> quickSort(
            Queue<Item> items) {
        // Your code here!
        if (items.size() <= 1) {
            return items;
        }
        Queue<Item> less = new Queue<>();
        Queue<Item> equal = new Queue<>();
        Queue<Item> greater = new Queue<>();
        partition(items, getRandomItem(items), less, equal, greater);
        less = quickSort(less);
        greater = quickSort(greater);
        items = catenate(catenate(less, equal), greater);
        return items;
    }
```

