### Abstraction

#### Counting sort

1. Create an int array called **counts** of size R (3 - cat / dog / person)
2. Iterate through the unsorted array, count the total number of each kind of elements
3. Create a new empty array called **sorted array**
4. Create a new array of size R called **starts** which can tell you where the first elements to go
5. Iterate throught the unsorted array and put them in the right spot of sorted array

* Non - negative integers
  * Systematic way

```java
	public static int[] naiveCountingSort(int[] arr) {
        // find max
        int max = Integer.MIN_VALUE;
        for (int i : arr) {
            max = max > i ? max : i;
        }

        // gather all the counts for each value
        int[] counts = new int[max + 1];
        for (int i : arr) {
            counts[i]++;
        }

        // when we're dealing with ints, we can just put each value
        // count number of times into the new array
        int[] sorted = new int[arr.length];
        int k = 0;
        for (int i = 0; i < counts.length; i += 1) {
            for (int j = 0; j < counts[i]; j += 1, k += 1) {
                sorted[k] = i;
            }
        }

        // however, below is a more proper, generalized implementation of
        // counting sort that uses start position calculation
        int[] starts = new int[max + 1];
        int pos = 0;
        for (int i = 0; i < starts.length; i += 1) {
            starts[i] = pos;
            pos += counts[i];
        }

        int[] sorted2 = new int[arr.length];
        for (int i = 0; i < arr.length; i += 1) {
            int item = arr[i];
            int place = starts[item];
            sorted2[place] = item;
            starts[item] += 1;
        }

        // return the sorted array
        return sorted;
    }
```

#### Radix Sort

* radix numeral system
* subroutine 子程序
* Casting
  * casting the `char` to an `int` (`int i = (int)'a'`)
  * char a = (char)97
* For Strings, the sort runs in `O(N*M)` time where `N` is the number of Strings and `M` is the length of the longest String

##### Sort Strings vs. Integer

* To sort Strings, we would pad them on the right with empty values
  * 2 > 100 (2 = 2__)
* To sort numbers, we would pad them on the left with empty values.

```java
public static String[] sort(String[] asciis) {
        // Implement LSD Sort
        String[] sorting = new String[asciis.length];
        for (int i = 0; i < asciis.length; i += 1) {
            sorting[i] = asciis[i];
        }
        int maxLength = 0;
        // find the max length in the String
        for (String s : sorting) {
            maxLength = maxLength > s.length() ? maxLength : s.length();
        }

        // Sorting the array digit by digit
        for (int d = maxLength - 1; d >= 0; d -= 1) {
            sortHelperLSD(sorting, d);
        }
        return sorting;
    }
```

helpmethod

```java
private static void sortHelperLSD(String[] asciis, int index) {
        // Optional LSD helper method for required LSD radix sort
        int[] counts = new int[256];
        for (String s : asciis) {
            if (s.length() - 1 < index) {
                counts[0] += 1;
            } else {
                counts[s.charAt(index)] += 1;
            }
        }

        // general way
        int[] starts = new int[256];
        int pos = 0;
        for (int i = 0; i < starts.length; i += 1) {
            starts[i] = pos;
            pos += counts[i];
        }

        String[] sorted = new String[asciis.length];
        for (int i = 0; i < asciis.length; i += 1) {
            String item = asciis[i];
            if (item.length() - 1 < index) {
                sorted[starts[0]] = item;
                starts[0] += 1;
            } else {
                int place = starts[item.charAt(index)];
                sorted[place] = item;
                starts[item.charAt(index)] += 1;
            }
        }
        for (int i = 0; i < asciis.length; i += 1) {
            asciis[i] = sorted[i];
        }

        return;
    }
```

