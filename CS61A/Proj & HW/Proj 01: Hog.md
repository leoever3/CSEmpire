### Dice game Hog



#### Abstraction

* Control statements
* High order functions



##### Phase 1: Simulator

##### Phase 2: Commentary

##### Phase 3: Strategies





> A new piece of Python syntax: We would like to write a function that accepts an **arbitrary number of arguments**, and then calls another function using exactly those arguments. Here's how it works.
>
> Instead of listing formal parameters for a function, you can write `*args`, which represents all of the **arg**ument**s** that get passed into the function. We can then call another function with these same arguments by passing these `*args` into this other function. For example:
>
> ```python
> >>> def printed(f):
> ...     def print_and_return(*args):
> ...         result = f(*args)
> ...         print('Result:', result)
> ...         return result
> ...     return print_and_return
> >>> printed_pow = printed(pow)
> >>> printed_pow(2, 8)
> Result: 256
> 256
> >>> printed_abs = printed(abs)
> >>> printed_abs(-10)
> Result: 10
> 10
> ```



##### Results



![image-20220528190514085](/Users/morningstar/Library/Application Support/typora-user-images/image-20220528190514085.png)