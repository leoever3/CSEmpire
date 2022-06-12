##### List

```python
>>> l = [1]

>>> l + [2]
[1, 2]

>>> l.append(2)
>>> l
[1, 2]

# Nested list
>>> l = [[1]]

>>> l + [[2]]
[[1], [2]]

>>> l.append([2])
>>> l
[[1], [2]]
```



###### [] with [None]

* `[]` is an empty list
* `[None]` is a list with one element. That one element is `None`

* `len([]) == 0`
* `len([None]) == 1`



#### Mutation operation for list

- `append(el)`: Add `el` to the end of the list. Return `None`.
- `extend(lst)`: Extend the list by concatenating it with `lst`. Return `None`.
- `insert(i, el)`: Insert `el` at index `i`. This does not replace any existing elements, but only adds the new element `el`. Return `None`.
- `remove(el)`: Remove the first occurrence of `el` in list. Errors if `el` is not in the list. Return `None` otherwise.
- `pop(i)`: Remove and return the element at index `i`.

[] + [] --> build a new list
