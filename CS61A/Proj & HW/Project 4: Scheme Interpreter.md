| Part                  | Problem | Abstraction                                                  | Function                    | File                                     |
| --------------------- | ------- | ------------------------------------------------------------ | --------------------------- | ---------------------------------------- |
| I.Evaluator           | 1       | Enable environment to define name-value pair                 | `define`, `look up`         | `scheme_classes.py`:  `Frame` class      |
|                       | 2       | Handle builtin procedure                                     | `scheme_apply`              | `scheme_eval_apply.py`                   |
|                       | 3       | Done: looks up names in the current environment, returns self-evaluating expressions (such as numbers) and evaluates special forms. <br />Todo: call expression | `scheme_eval`               | `scheme_eval_apply.py`                   |
|                       | 4       | Enable special form: define name value                       | `do_define_form`            | `scheme_forms.py`                        |
|                       | 5       | Enable special form: quote                                   | `do_quote_form`             | `scheme_forms.py`                        |
| II.Procedure          | 6       | implementation of the `begin` special form                   | `eval_all`                  | `scheme_eval_apply.py`                   |
|                       | 7       | Evaluate a lambda form.                                      | `do_lambda_form`            | `scheme_forms.py`                        |
|                       | 8       | Enable user-defined function to create new frame             | `make_child_frame`          | `scheme_classes.py`:  `Frame` class      |
|                       | 9       | Enable lambda function definition                            | `scheme_apply`              | `scheme_eval_apply.py`                   |
|                       | 10      | Enable shorthand form of defining                            | `do_define_form`            | `scheme_forms.py`                        |
|                       | 11      | dynamic scoping function `mu`                                | `do_mu_form` `scheme_apply` | `scheme_forms.py` `scheme_eval_apply.py` |
| III. Special Form     | 12      | `and` & `or` special form                                    | `do_and_form` `do_or_form`  | `scheme_forms.py`                        |
|                       | 13      | `cond` special form                                          | `do_cond_form`              | `scheme_forms.py`                        |
|                       | 14      | `let` special form                                           | `make_let_frame`            | `scheme_forms.py`                        |
| IV. Write some scheme | 15      | scheme problem                                               |                             | `question.scm`                           |
|                       | 16      | scheme problem                                               |                             | `question.scm`                           |
|                       |         |                                                              |                             |                                          |
|                       |         |                                                              |                             |                                          |



### Project 4: Scheme Interpreter

#### Part I: The Evaluator

- Symbol evaluation
- Calling built-in procedures
- Definitions

Finished:

* numbers, booleans, and `nil`.



These are all of the essential components of the interpreter. `scheme_forms.py` defines special forms, `scheme_builtins.py` defines the various functions built into the standard library, and `scheme.py` defines input/output behavior.



###### Questions

Q1: What types of expressions are represented as Pairs?
Choose the number of the correct choice:

0) All expressions are represented as Pairs
1) Only call expressions
2) Call expressions and special forms
3) Only special forms
? 2
-- OK! --

Q2: What expression in the body of scheme_eval finds the value of a name?
Choose the number of the correct choice:

0) scheme_forms.SPECIAL_FORMS[first](rest, env)
1) scheme_symbolp(expr)
2) env.lookup(expr)
3) env.find(name)
? 2
-- OK! --

Q3: How do we know if a given combination is a special form?
Choose the number of the correct choice:
0) Check if the first element in the list is a symbol
1) Check if the first element in the list is a symbol and that the
   symbol is in the dictionary SPECIAL_FORMS
2) Check if the expression is in the dictionary SPECIAL_FORMS
? 1

Q4: What is the difference between applying builtins and applying user-defined procedures?
(Choose all that apply)

I.   User-defined procedures open a new frame; builtins do not
II.  Builtins simply execute a predefined function; user-defined
     procedures must evaluate additional expressions in the body
III. Builtins have a fixed number of arguments; user-defined procedures do not

Choose the number of the correct choice:
0) III only
1) II only
2) I only
3) I, II and III
4) I and II
5) I and III
6) II and III
? 4
-- OK! --

Q5: What exception should be raised for the expression (1)?
Choose the number of the correct choice:

0) SchemeError("malformed list: (1)")
1) AssertionError
2) SchemeError("unknown identifier: 1")
3) SchemeError("1 is not callable")

? 3
-- OK! --



Problem 4 > Suite 1 > Case 1

Q: What is the structure of the expressions argument to do_define_form?
Choose the number of the correct choice:

0) Pair(A, B), where:
       A is the symbol being bound,
       B is an expression whose value should be evaluated and bound to A
1) Pair('define', Pair(A, Pair(B, nil))), where:
       A is the symbol being bound,
       B is an expression whose value should be evaluated and bound to A
2) Pair(A, Pair(B, nil)), where:
       A is the symbol being bound,
       B is an expression whose value should be evaluated and bound to A
3) Pair(A, Pair(B, nil)), where:
       A is the symbol being bound,
       B is the value that should be bound to A
4) Pair(A, B), where:
       A is the symbol being bound,
       B is the value that should be bound to A

​	   ? 2

Problem 4 > Suite 1 > Case 2

Q: What method of a Frame instance will bind
a value to a symbol in that frame?
Choose the number of the correct choice:

0) bindings
1) define
2) lookup
3) make_child_frame
? 1

Problem 5 > Suite 1 > Case 1
(cases remaining: 4)

Q: What is the structure of the expressions argument to do_quote_form?
Choose the number of the correct choice:
0) A, where:
       A is the quoted expression
1) [A], where:
       A is the quoted expression
2) Pair('quote', Pair(A, nil)), where:
       A is the quoted expression
3) Pair(A, nil), where:
       A is the quoted expression
   ? 3



expr = Pair(Pair('+', Pair('x', Pair(2, nil))), nil)
do_quote_form(expr, global_frame) # Make sure to use Pair notation
? ((+ x 2))
-- Not quite. Try again! --

? Pair('+', Pair('x', Pair(2, nil)))
-- OK! --



scm> ''hello

Choose the number of the correct choice:

0) (quote (quote (hello)))
1) hello
2) (hello)
3) (quote hello)
? 3
-- OK! --



scm> (cons 'car '('(4 2)))
? (car (quote (4 2)))



#### Part II: Procedures

In Part II, you will add the ability to create and call user-defined procedures. You will add the following features to the interpreter:

- Lambda procedures, using the `(lambda ...)` special form
- Named lambda procedures, using the `(define (...) ...)` special form
- Mu procedures, with *dynamic scope*

###### User-Defined Procedures

User-defined lambda procedures are represented as instances of the `LambdaProcedure` class. A `LambdaProcedure` instance has three instance attributes:

- `formals` is a Scheme list of the formal parameters (symbols) that name the arguments of the procedure.
- `body` is a Scheme list of expressions; the body of the procedure.
- `env` is the environment in which the procedure was **defined**.





Problem 7 > Suite 2 > Case 1
(cases remaining: 2)

```python
from scheme_reader import *
from scheme import *
env = create_global_frame()
lambda_line = read_line("(lambda (a b c) (+ a b c))")
lambda_proc = do_lambda_form(lambda_line.rest, env)
>>> lambda_proc.formals # use single quotes ' around strings in your answer
Pair('a', Pair('b', Pair('c', nil)))

>>> lambda_proc.body # the body is a *list* of expressions! Make sure your answer is a properly nested Pair.
Pair(Pair('+', Pair('a', Pair('b', Pair('c', nil)))), nil)
```



## Part III: Special Forms

Logical special forms include `if`, `and`, `or`, and `cond`. These expressions are special because not all of their sub-expressions may be evaluated.

In Scheme, only `#f` is a false value. All other values (including `0` and `nil`) are true values. You can test whether a value is a true or false value using the provided Python functions `is_scheme_true` and `is_scheme_false`, defined in `scheme_builtins.py`.

> Scheme traditionally uses `#f` to indicate the false Boolean value. In our interpreter, that is equivalent to `false` or `False`. Similarly, `true`, `True`, and `#t` are all equivalent. However when unlocking tests, use `#t` and `#f`.

To get you started, we've provided an implementation of the `if` special form in the `do_if_form` function. Make sure you understand that implementation before starting the following questions.





scm> (and)
#t

scm> (or)

#f



#### Part IV: Write Some Scheme

![image-20220705145750739](/Users/morningstar/Library/Application Support/typora-user-images/image-20220705145750739.png)