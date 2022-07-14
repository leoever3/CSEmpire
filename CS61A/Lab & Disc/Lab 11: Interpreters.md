# Introduction

In the [Scheme project](https://cs61a.org/proj/scheme/), you'll be implementing a Python interpreter for Scheme.

Part of the process of interpreting Scheme expressions is being able to **parse** a string of Scheme code as our input into our interpreter's internal Python representation of Scheme expressions. As all Scheme expressions are Scheme lists (and therefore linked lists), we represent all Scheme expressions using the `Pair` class, which behaves as a linked list. **This class is defined in `pair.py`.**

When given an input such as `(+ 1 2)`, there are two main steps we want to take.

The first part of interpreting expressions is taking the input and breaking it down into each component. In our example, we want to treat each of `(`, `+`, `1`, `2`, and `)` as a separate token that we can then figure out how to represent. This is called **lexical analysis**, and has been implemented for you in the `tokenize_lines` function in `scheme_tokens.py`.

Now that we've broken down the input into its component parts, we want to turn these Scheme tokens into our interpreter's internal representations of them. This is called **syntactic analysis**, which happens in `scheme_reader.py` in the `scheme_read` and `read_tail` functions.

- `(` tells us we are starting a call expression.
- `+` will be the operator, as it's the first element in the call expression.
- `1` is our first operand.
- `2` is our second operand.
- `)` tells us that we are ending the call expression.

The main idea is that we'd like to first recognize what the input represents, before we do any of the evaluating, or calling the operator on the operands, and so on.

The goal of this lab is to work with the various parts that go into parsing; while in this lab and in the project, we're focusing on the Scheme language, the general ideas of how we're setting up the Scheme interpreter can be applicable to other languages -- such as Python itself!





### Context

We store tokens ready to be parsed in `Buffer` instances. For example, a buffer containing the input `(+ (2 3))` would have the tokens `'('`, `'+'`, `'('`, `2`, `3`, `')'`, and `')'`.

In this part, we will implement the `Buffer` class.

A `Buffer` provides a way of accessing a sequence of tokens across lines.

Its constructor takes an iterator, called "the `source`", that returns the next line of tokens as a list each time it is queried, until it runs out of lines.

For example, `source` could be defined as shown:

```python
line1 = ['(', '+', 6, 1 ')']      # (+ 6 1)
line2 = ['(', 'quote', 'A', ')']  # (quote A)
line3 = [2, 1, 0]                 # 2 1 0
input_lines = [line1, line2, line3]
source = iter(input_lines)
```

The `Buffer` in effect concatenates the sequences returned from its source and then supplies the items from them one at a time through its `pop_first` method, calling the `source` for more sequences of items only when needed.

In addition, `Buffer` provides a `current` method to look at the next item to be supplied, without sequencing past it.



### Internal Representations

The reader will parse Scheme code into Python values with the following representations:

| Input Example  | Scheme Expression Type | Our Internal Representation                                  |
| :------------- | :--------------------- | :----------------------------------------------------------- |
| `scm> 1`       | Numbers                | Python's built-in `int` and `float` values                   |
| `scm> x`       | Symbols                | Python's built-in `string` values                            |
| `scm> #t`      | Booleans (`#t`, `#f`)  | Python's built-in `True`, `False` values                     |
| `scm> (+ 2 3)` | Combinations           | Instances of the `Pair` class, defined in `scheme_reader.py` |
| `scm> nil`     | `nil`                  | The `nil` object, defined in `scheme_reader.py`              |

When we refer to combinations here, we are referring to both call expressions and special forms.