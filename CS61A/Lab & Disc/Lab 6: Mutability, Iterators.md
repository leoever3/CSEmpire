## Iterators

An iterable is any object that can be iterated through, or gone through one element at a time. One construct that we've used to iterate through an iterable is a for loop:

```
for elem in iterable:
    # do something
```

`for` loops work on any object that is *iterable*. We previously described it as working with any sequence -- all sequences are iterable, but there are other objects that are also iterable! We define an **iterable** as an object on which calling the built-in function `iter` function returns an *iterator*. An **iterator** is another type of object that allows us to iterate through an iterable by keeping track of which element is next in the sequence.

To illustrate this, consider the following block of code, which does the exact same thing as the `for` statement above:

```
iterator = iter(iterable)
try:
    while True:
        elem = next(iterator)
        # do something
except StopIteration:
    pass
```

Here's a breakdown of what's happening:

- First, the built-in `iter` function is called on the iterable to create a corresponding *iterator*.
- To get the next element in the sequence, the built-in `next` function is called on this iterator.
- When `next` is called but there are no elements left in the iterator, a `StopIteration` error is raised. In the for loop construct, this exception is caught and execution can continue.

Calling `iter` on an iterable multiple times returns a new iterator each time with distinct states (otherwise, you'd never be able to iterate through a iterable more than once). You can also call `iter` on the iterator itself, which will just return the same iterator without changing its state. However, note that you cannot call `next` directly on an iterable.

Let's see the `iter` and `next` functions in action with an iterable we're already familiar with -- a list.

```
>>> lst = [1, 2, 3, 4]
>>> next(lst)             # Calling next on an iterable
TypeError: 'list' object is not an iterator
>>> list_iter = iter(lst) # Creates an iterator for the list
>>> list_iter
<list_iterator object ...>
>>> next(list_iter)       # Calling next on an iterator
1
>>> next(list_iter)       # Calling next on the same iterator
2
>>> next(iter(list_iter)) # Calling iter on an iterator returns itself
3
>>> list_iter2 = iter(lst)
>>> next(list_iter2)      # Second iterator has new state
1
>>> next(list_iter)       # First iterator is unaffected by second iterator
4
>>> next(list_iter)       # No elements left!
StopIteration
>>> lst                   # Original iterable is unaffected
[1, 2, 3, 4]
```

Since you can call `iter` on iterators, this tells us that that they are also iterables! Note that while all iterators are iterables, the converse is not true - that is, not all iterables are iterators. You can use iterators wherever you can use iterables, but note that since iterators keep their state, they're only good to iterate through an iterable once:

```
>>> list_iter = iter([4, 3, 2, 1])
>>> for e in list_iter:
...     print(e)
4
3
2
1
>>> for e in list_iter:
...     print(e)
```

> **Analogy**: An iterable is like a book (one can flip through the pages) and an iterator for a book would be a bookmark (saves the position and can locate the next page). Calling `iter` on a book gives you a new bookmark independent of other bookmarks, but calling `iter` on a bookmark gives you the bookmark itself, without changing its position at all. Calling `next` on the bookmark moves it to the next page, but does not change the pages in the book. Calling `next` on the book wouldn't make sense semantically. We can also have multiple bookmarks, all independent of each other.



## Mutability

We say that an object is **mutable** if its state can change as code is executed. The process of changing an object's state is called **mutation**. Examples of mutable objects include lists and dictionaries. Examples of objects that are *not* mutable include tuples and functions.



### Q1: WWPD: List-Mutation

```python
>>> lst = [5, 6, 7, 8]
>>> lst.append(6)
Nothing

>>> lst
[5, 6, 7, 8, 6]

>>> lst.insert(0, 9)
>>> lst
[9, 5, 6, 7, 8, 6]

>>> x = lst.pop(2) # pop the element with index 2
>>> lst
[9, 5, 7, 8, 6]

>>> lst.remove(x) # remove x in the list
>>> lst
[9, 5, 7, 8]

>>> a, b = lst, lst[:]
>>> a is lst
True

>>> b == lst
True

>>> b is lst
False

>>> lst = [1, 2, 3]
>>> lst.extend([4,5])
>>> lst
[1, 2, 3, 4, 5]

>>> lst.extend([lst.append(9), lst.append(10)])
>>> lst
[1, 2, 3, 4, 5, 9, 10, None, None]
```

### Q3: WWPD: Iterators

```python
>>> s = [1, 2, 3, 4]
>>> t = iter(s)
>>> next(s)
Error

>>> next(t)
1

>>> next(t)
2

>>> iter(s)
Error

>>> next(iter(s))
1

>>> next(iter(t))
3

>>> next(iter(s))
1

>>> next(iter(t))
4

>>> next(t)
StopIteration



>>> r = range(6)
>>> r_iter = iter(r)
>>> next(r_iter)
0

>>> [x + 1 for x in r]
[1, 2, 3, 4, 5, 6]

>>> [x + 1 for x in r_iter]
[2, 3, 4, 5, 6]

>>> next(r_iter)
StopIteration

>>> list(range(-2, 4))   # Converts an iterable into a list
[-2, -1, 0, 1, 2, 3]


>>> map_iter = map(lambda x : x + 10, range(5))
>>> next(map_iter)
10

>>> next(map_iter)
11

>>> list(map_iter)
[12, 13, 14]

>>> for e in filter(lambda x : x % 2 == 0, range(1000, 1008)):
...     print(e)
1000
1002
1004
1006

>>> [x + y for x, y in zip([1, 2, 3], [4, 5, 6])]
[5, 7, 9]

>>> for e in zip([10, 9, 8], range(3)):
...   print(tuple(map(lambda x: x + 2, e)))
(12, 2)
(11, 3)
(10, 4)

>>> list(zip([10, 9, 8], range(3)))
[(10, 0), (9, 1), (8, 2)]
```



"in a row" means continuously