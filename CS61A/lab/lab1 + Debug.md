##### Division, Floor Div, and Module

1 / 5 = 0.2

1 // 5 = 0

1 % 5 = 1

##### Function

* Abstraction
* Call expression

##### Control

* Boolean
* If
* While

### Control

##### Print & Return

* Notice also that `print` will display text **without the quotes**, but `return` will preserve the quotes.

##### True or False

* 0 -- false

* Positive/negative -- true

### Veritasiness

```python
>>> True and 13
13

>>> not 10
False

>>> True and 1 / 0 and False
Error

>>> 1 and 3 and 6 and 10 and 15
15
```

### Debug

#### Traceback messages

**First line**

```
File "<file name>", line <number>, in <function>
```

**Second line**

Actual line of code

```python
    result = buggy(5)
```

* The most recent function call at the bottom

#### Error messages

```python
<error type>: <error message>
```



#### Debugging Techniques

##### Running doctest

```bash
python3 -m doctest file.py

python3 -m doctest file.py -v
```

```python
def square(x):
       '''
       >>> square(2)
       4
       '''
       return x * x
```

##### Writing you own tests

* Test-driven development
* Write more tests after you write code
* Test edge cases

##### Using print statement

```python
 print('DEBUG: other_function returns', tmp)
```

##### Long-term debugging

* **Global debug variable**

```python
debug = True

def foo(n):
i = 0
while i < n:
    i += func(i)
    if debug:
        print('DEBUG: i is', i)
```

##### Interactive debugging

```bash
python -i file.py

python ok -q ### Q1: name -i

python3 ok -q sum_digits -i
```

##### PythonTutor debugging

* Environment diagram

```bash
python ok -q ### Q2: name --trace

python3 ok -q sum_digits --trace
```

##### Using assert statement

```python
def double(x):
    assert isinstance(x, int), "The input to double(x) must be an integer"
    return 2 * x
```

* It is generally **good** practice to release code with assertion statements left in

### Error

#### Error types

* SyntaxError
* IndentationError
* TypeError
* NameError
  * is not defined
* IndexError
  * Array

#### Common Bugs

* Spelling
* Missing Parentheses
* Missing close quotes
* **= VS. ==**
* Infinite Loops
* Off-by-one errors