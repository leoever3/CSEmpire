### Lambda Expressions

```python
lambda <parameters>: <return expression>
```

### Environment Diagrams

#### Assignment Statements

1. Evaluate the expression on the right hand side of the `=` sign.
2. If the name found on the left hand side of the `=` doesn't already exist in the current frame, write it in. If it does, erase the current binding. Bind the *value* obtained in step 1 to this name.

#### def Statements

1. Draw the function object with its intrinsic name, formal parameters, and parent frame. A function's parent frame is the frame in which the function was defined.
2. If the intrinsic name of the function doesn't already exist in the current frame, write it in. If it does, erase the current binding. Bind the newly created function object to this name.

#### Call expressions

1. Evaluate the operator, whose value should be a function.
2. Evaluate the operands left to right.
3. Open a new frame. Label it with **the sequential frame number, the intrinsic name of the function, and its parent.**
4. Bind the formal parameters of the function to the arguments whose values you found in step 2.
5. Execute the body of the function in the new environment.



### Tips

```python
>>> (lambda: 3)()

3
```



```python
>>> def cake():
...    print('beets')
...    def pie():
...        print('sweets')
...        return 'cake'
...    return pie

>>> chocolate = cake()
? beets

>>> chocolate
? Function

>>> chocolate() # chocolate is bound to pie
(line 1)? sweets
(line 2)? 'cake'

>>> more_chocolate, more_cake = chocolate(), cake
? sweets

>>> more_chocolate
? 'cake'

>>> def snake(x, y):
...    if cake == more_cake:
...        return chocolate
...    else:
...        return x + y
>>> snake(10, 20)
? Function

>>> snake(10, 20)()
(line 1)? sweets
(line 2)? 'cake'
-- OK! --

>>> cake = 'cake'
>>> snake(10, 20)
? 30
```



##### Amazing problem

![image-20211229155232452](/Users/morningstar/Library/Application Support/typora-user-images/image-20211229155232452.png)

Because I have a **i = i + 1** on the next two lines, so python treat. i as a local variable in the innerhelper. And for the remainder and quotient, because there is no R and Q in the left side of the =, so python look for these two variable upside and works fine.

https://stackoverflow.com/questions/370357/unboundlocalerror-on-local-variable-when-reassigned-after-first-use