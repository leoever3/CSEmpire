### Lambda expressions

```python
>>> what = lambda x : x + 5
>>> what
<function <lambda> at 0xf3f490>
```

### Higher order Functions

* A **higher order function** (HOF) is a function that manipulates other functions by taking in functions as arguments, returning a function, or both.

#### HOFs in Environment Diagrams

* An **environment diagram** keeps track of all the variables that have been defined and the values they are bound to.



### Self Reference

* Self-reference refers to a particular design of HOF, where a function eventually returns itself.
  * f(5)(2)(3)(4)(6)(7887)(3)(5)(7)(9)

```python
def match_k(k):
    """ Return a function that checks if digits k apart match

    >>> match_k(2)(1010)
    True
    >>> match_k(2)(2010)
    False
    >>> match_k(1)(1010)
    False
    >>> match_k(1)(1)
    True
    >>> match_k(1)(2111111111111111)
    False
    >>> match_k(3)(123123)
    True
    >>> match_k(2)(123123)
    False
    """
    def helper(x):
        while x // (10 ** k):
            if x % 10 != (x // (10 ** k)) % 10:
                return False
            x = x // 10
        return True
    return helper
```

```python
def three_memory(n):
    """
    >>> f = three_memory('first')
    >>> f = f('first')
    Not found
    >>> f = f('second')
    Not found
    >>> f = f('third')
    Not found
    >>> f = f('second') # 'second' was not input three calls ago
    Not found
    >>> f = f('second') # 'second' was input three calls ago
    Found
    >>> f = f('third') # 'third' was input three calls ago
    Found
    >>> f = f('third') # 'third' was not input three calls ago
    Not found
    """
    def f(x, y, z):
        def g(i):
            if i == x:
                print('Found')
            else:
                print('Not found')
            return f(y, z, i)
        return g
    return f(None, None, n)
```

```python
def chain_function():
    """
    >>> tester = chain_function()
    >>> x = tester(1)(2)(4)(5) # Expected 3 but got 4, so print 3. 1st chain break, so print 1 too.
    3 1
    >>> x = x(2) # 6 should've followed 5 from above, so print 6. 2nd chain break, so print 2
    6 2
    >>> x = x(8) # The chain restarted at 2 from the previous line, but we got 8. 3rd chain break.
    3 3
    >>> x = x(3)(4)(5) # Chain restarted at 8 in the previous line, but we got 3 instead. 4th break
    9 4
    >>> x = x(9) # Similar logic to the above line
    6 5
    >>> x = x(10) # Nothing is printed because 10 follows 9.
    >>> y = tester(4)(5)(8) # New chain, starting at 4, break at 6, first chain break
    6 1
    >>> y = y(2)(3)(10) # Chain expected 9 next, and 4 after 10. Break 2 and 3.
    9 2
    4 3
    """
    def g(x, y): 
        # x: expected num, y: count
        def h(n):
            if x == 0 or n == x:
                return g(n + 1, y)
            else:
                # BEGIN SOLUTION ALT="return ____________________________" NO PROMPT
                return print(x, y + 1) or g(n + 1, y + 1)
                # print() returns None so it always execute g(n + 1, y + 1) to restart our chain
        return h
```

