#### Setup

* Install a terminal
* Install python 3
* Install a text editon (VScode)



#### Terminal

```bash
$ python3
>>> exit() or ctrl + D
```

- `ls`: lists all files in the current directory
- `cd <path to directory>`: change into the specified directory
- `mkdir <directory name>`: make a new directory with the given name
- `mv <source path> <destination path>`: move the file at the given source to the given destination



#### <u>Python command line options</u>

```bash
python3 lab00.py # execute the py file

python3 -i lab00.py # run interactively

python3 -m doctest lab00.py # -m doctest: Runs doctests in a particular file. Doctests are surrounded by triple quotes (""") within functions.

python3 -m doctest -v lab00.py # show details
```



#### Python Basic

##### Expressions and Statements

* An **expression** is a piece of code that evaluates to some value
  * Primitive expression
  * Arithmetic expression
* A **statement** is one or more lines of code that make something happen in a program
  * Assignment statements

##### Math

* True division
  * /
* Floor div -- integer division
  * //
* Module
  * %



#### Functions

* If we want to execute a series of statements over and over again, we can **abstract** them away into a function to avoid repeating code
* `def` -- `return`

##### Call expressions

* A call expression applies a function which may accept arguments
* The call expression **evaluates** to the function's return value

```python
  add   (    2   ,    3   )
   |         |        |
operator  operand  operand
```

* To evaluate a function call
  * Evaluate the **operator** and then the **operands**(from left to right)
  * Apply the operator to the operands(the values of the operands)
* **Nested** call expression
  * Inner operand first



##### Control

##### Boolean operators

* `True` and `False`
  * False: 0, None, '', [] (empty string/list)
* and, or, not

##### Short Circuiting



##### If statment

* `If, elif, else`

##### While loops



##### Error Messages

| Error Types       | Descriptions                                                 |
| :---------------- | :----------------------------------------------------------- |
| SyntaxError       | Contained improper syntax (e.g. missing a colon after an `if` statement or forgetting to close parentheses/quotes) |
| IndentationError  | Contained improper indentation (e.g. inconsistent indentation of a function body) |
| TypeError         | Attempted operation on incompatible types (e.g. trying to add a function and a number) or called function with the wrong number of arguments |
| ZeroDivisionError | Attempted division by zero                                   |



#### Lambda Expressions

* Lambda expressions are expressions that evaluate to **functions** by specifying two things: the parameters and a return expression.

```python
lambda <parameters>: <return expression>
```

##### Environment Diagrams

* An **environment diagram** keeps track of all the variables that have been defined and the values they are bound to.

##### Assignment Statements

1. Evaluate the expression on the right hand side of the `=` sign.
2. If the name found on the left hand side of the `=` doesn't already exist in the current frame, write it in. If it does, erase the current binding. Bind the *value* obtained in step 1 to this name.

##### def Statement

1. Draw the function object with its **intrinsic** name, **formal parameters**, and **parent frame**. A function's parent frame is the frame in **which the function was defined**.
2. If the intrinsic name of the function doesn't already exist in the current frame, write it in. If it does, erase the current binding. Bind the newly created function object to this name.

##### Call expressions

1. Evaluate the operator, whose value should be a function.
2. Evaluate the operands left to right.
3. Open a new frame. Label it with **the sequential frame number, the intrinsic name of the function, and its parent.**
4. Bind the formal parameters of the function to the arguments whose values you found in step 2.
5. Execute the body of the function in the new environment.

![image-20211229140801776](/Users/morningstar/Library/Application Support/typora-user-images/image-20211229140801776.png)

##### Lambdas

1. Draw the lambda function object and label it with λ, its formal parameters, and its parent frame. A function's parent frame is the frame in which the function was defined.

##### Currying

* We can transform multiple-argument functions into a chain of single-argument, higher order functions by taking advantage of lambda expressions
* we can write a function `f(x, y)` as a different function `g(x)(y)`



#### Midterm Review

###### What would python print

* The `print` function return `none`
* It also displays its arguments seperated by spaces when it is called

| This expression | Evaluates to | Interactive output |
| --------------- | ------------ | ------------------ |
| 5               | 5            | 5                  |
| print(5)        | None         | 5                  |
| print(print(5)) | None         | 5 \ None           |