## Install

###### Terminal: 

If you're on a Mac or are using a form of Linux (such as Ubuntu), you already have a program called `Terminal` or something similar on your computer. 

###### Python3:

Install python 3.10.0

`$ python3 --version`

###### Text editor: **Visual Studio Code**

- [Visual Studio Code](https://inst.eecs.berkeley.edu/~cs61a/fa21/articles/vscode): A full-featured desktop editor with many extensions available to support different languages.
- [Atom](https://inst.eecs.berkeley.edu/~cs61a/fa21/articles/atom): A more lightweight desktop editor.
- [Vim](https://inst.eecs.berkeley.edu/~cs61a/fa21/articles/vim): A command-line editor.
- [Emacs](https://inst.eecs.berkeley.edu/~cs61a/fa21/articles/emacs): A command-line editor.

A few other editors:

- [PyCharm](https://www.jetbrains.com/pycharm/): A desktop editor designed for Python.
- [Sublime Text](https://www.sublimetext.com/): A text editor that works with code.



## Terminal

##### Python interpreter

```bash
$ python3
>>>

>>> exit()
>>> ctrl D
```

##### Organize files

> `$ clear`: Clear the screen
>
> `$ ls`: List all the files
>
> `$ cd`: Change directory
>
> - `cd ..` (two dots). The `..` means "the parent directory". In this case, the parent directory of `cs61a` is your home directory, so you can use `cd ..` to go up one directory.
> - `cd ~` (the tilde). Remember that `~` means home directory, so this command will always change to your home directory.
> - `cd` (`cd` on its own). Typing just `cd` is a shortcut for typing `cd ~`
>
> `pwd`: Print working directory
>
> `unzip lab00.zip`
>
> `mv ~/Downloads/lab00 ~/cs61a/lab
>
> 

###### Summary

- `ls`: lists all files in the current directory
- `cd <path to directory>`: change into the specified directory
- `mkdir <directory name>`: make a new directory with the given name
- `mv <source path> <destination path>`: move the file at the given source to the given destination

[UNIX tutorial](https://inst.eecs.berkeley.edu/~cs61a/fa20/articles/unix.html)



# Python Basics

#### Expressions and statements

Programs are made up of expressions and statements. An *expression* is a piece of code that evaluates to some value and a *statement* is one or more lines of code that make something happen in a program.

When you enter a Python expression into the interactive Python interpreter, its value will be displayed. As you read through the following examples, try out some similar expressions on your own Python interpreter, which you can start up by typing this in your terminal:

```bash
python3
```

> Remember, if you are using Windows and the `python3` command doesn't work, try using `python` or `py`. See the [install Python 3](https://inst.eecs.berkeley.edu/~cs61a/fa21/lab/lab00/#install-python-3) section for more info and ask for help if you get stuck!



### Primitive expressions

Primitive expressions only take one step to evaluate. These include numbers and booleans, which just evaluate to themselves.

```python
>>> 3
3
>>> 12.5
12.5
>>> True
True
```

### Arithmetic expressions

Numbers may be combined with mathematical operators to form compound expressions. In addition to the `+` operator (addition), the `-` operator (subtraction), the `*` operator (multiplication) and the `**` operator (exponentiation), there are three division-like operators to remember:

- Floating point division (`/`): divides the first number number by the second, evaluating to a number with a decimal point *even if the numbers divide evenly*.
- Floor division (`//`): divides the first number by the second and then rounds down, evaluating to an integer.
- Modulo (`%`): evaluates to the positive remainder left over from division.

Parentheses may be used to group subexpressions together; the entire expression is evaluated in PEMDAS (Parentheses, Exponentiation, Multiplication / Division, Addition / Subtraction) order.

```python
>>> 7 / 4
1.75
>>> (2 + 6) / 4
2.0
>>> 7 // 4        # Floor division (rounding down)
1
>>> 7 % 4         # Modulus (remainder of 7 // 4)
3
```







### Understanding problems

The lines in the triple-quotes `"""` are called a **docstring**, which is a description of what the function is supposed to do.

The lines that begin with `>>>` are called **doctests**



## Appendix: Useful Python command line options

When running a Python file, you can use options on the command line to inspect your code further. Here are a few that will come in handy. If you want to learn more about other Python command-line options, take a look at the [documentation](https://docs.python.org/3.9/using/cmdline.html).

- Using no command-line options will run the code in the file you provide and return you to the command line. For example, if we want to run `lab00.py` this way, we would write in the terminal:

  ```bash
  python3 lab00.py
  ```

- **`-i`**: The `-i` option runs your Python script, then opens an interactive session. In an interactive session, you run Python code line by line and get immediate feedback instead of running an entire file all at once. To exit, type `exit()` into the interpreter prompt. You can also use the keyboard shortcut `Ctrl-D` on Linux/Mac machines or `Ctrl-Z Enter` on Windows.

  If you edit the Python file while running it interactively, you will need to exit and restart the interpreter in order for those changes to take effect.

  Here's how we can run `lab00.py` interactively:

  ```bash
  python3 -i lab00.py
  ```

- **`-m doctest`**: Runs doctests in a particular file. Doctests are surrounded by triple quotes (`"""`) within functions.

  Each test in the file consists of `>>>` followed by some Python code and the expected output (though the `>>>` are not seen in the output of the doctest command).

  To run doctests for `lab00.py`, we can run:

  ```bash
   python3 -m doctest lab00.py
  ```
