### Install

Install python 3.10.0

Install text editor: **Visual Studio Code**

### *Terminal:*

```
$ echo "$HOME"
/Users/morningstar
```

~: Home Directory

```
$ python3
>>>

$ exit()
```

Python

```
$ clear
```

Clear the screen

```
$ ls
```

List all the files

```
$ cd
```

Change diretory

- `cd ..` (two dots). The `..` means "the parent directory". In this case, the parent directory of `cs61a` is your home directory, so you can use `cd ..` to go up one directory.
- `cd ~` (the tilde). Remember that `~` means home directory, so this command will always change to your home directory.
- `cd` (`cd` on its own). Typing just `cd` is a shortcut for typing `cd ~`

```
$ pwd
```

Print working directory

```
unzip lab00.zip
```

Unzip

```
mv ~/Downloads/lab00 ~/cs61a/lab
```

Move

#### Summary

- `ls`: lists all files in the current directory
- `cd <path to directory>`: change into the specified directory
- `mkdir <directory name>`: make a new directory with the given name
- `mv <source path> <destination path>`: move the file at the given source to the given destination

[UNIX tutorial](https://inst.eecs.berkeley.edu/~cs61a/fa20/articles/unix.html)

### Python Basics

```
python3
```

##### Primitive expressions

##### Arithmetic expressions

##### Assignment statements

/ & //

6 / 4 = 1.5

6 // 4 = 1

### Assignment

```
python3 ok -q python-basics -u
```

##### Understanding problems

The lines in the triple-quotes `"""` are called a **docstring**, which is a description of what the function is supposed to do.

The lines that begin with `>>>` are called **doctests**

### Appendix: Useful Python command line options

```bash
$ python3
$ python3 -i
$ python3 -m doctest
```

 

```bash
$ python3 -i ex.py
```

