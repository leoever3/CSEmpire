# Data Abstraction

Data abstraction is a powerful concept in computer science that allows programmers to treat code as objects. For example, using code to represent cars, chairs, people, and so on. That way, programmers don't have to worry about *how* code is implemented; they just have to know *what* it does.

Data abstraction mimics how we think about the world. If you want to drive a car, you don't need to know how the engine was built or what kind of material the tires are made of to do so. You just have to know how to use the car for driving itself, such as how to turn the wheel or press the gas pedal.

A data abstraction consists of two types of functions:

- **Constructors**: functions that build the abstract data type.
- **Selectors**: functions that retrieve information from the data type.

Programmers design data abstractions to abstract away how information is stored and calculated such that the end user does *not* need to know how constructors and selectors are implemented. The nature of *abstraction* allows whoever uses them to assume that the functions have been written correctly and work as described.

# Trees

One example of data abstraction is with **trees**.

In computer science, **trees** are recursive data structures that are widely used in various settings and can be implemented in many ways. The diagram below is an example of a tree.

![Example Tree](https://inst.eecs.berkeley.edu/~cs61a/fa21/disc/disc05/assets/example_tree_construction.png)

Generally in computer science, you may see trees drawn "upside-down" like so. We say the **root** is the node where the tree begins to branch out at the top, and the **leaves** are the nodes where the tree ends at the bottom.

Some terminology regarding trees:

- **Parent Node**: A node that has at least one branch.
- **Child Node**: A node that has a parent. A child node can only have one parent.
- **Root**: The top node of the tree. In our example, this is the `1` node.
- **Label**: The value at a node. In our example, every node's label is an integer.
- **Leaf**: A node that has no branches. In our example, the `4`, `5`, `6`, `2` nodes are leaves.
- **Branch**: A subtree of the root. Trees have branches, which are trees themselves: this is why trees are *recursive* data structures.
- **Depth**: How far away a node is from the root. We define this as the number of edges between the root to the node. As there are no edges between the root and itself, the root has depth 0. In our example, the `3` node has depth 1 and the `4` node has depth 2.
- **Height**: The depth of the lowest (furthest from the root) leaf. In our example, the `4`, `5`, and `6` nodes are all the lowest leaves with depth 2. Thus, the entire tree has height 2.

In computer science, there are many different types of trees, used for different purposes. Some vary in the number of branches each node has; others vary in the structure of the tree.

## Tree Data Abstraction

A tree has a root value and a list of branches, where each branch is itself a tree.

The data abstraction specifies that calling `branches` on a tree `t` will give us a **list of branches**. Treating the return value of `branches(t)` as a list is then part of how we define trees.

How the entire tree `t` is implemented is under the abstraction barrier. Rather than assuming an implementation of `label` and `branches`, we will want to use those selector functions directly.

For example, we could choose to implement the tree data abstraction with a dictionary with separate entries for the `label` and the `branches`, or as a list with the first element being `label` and the rest being `branches`.

- The `tree` constructor takes in a value `label` for the root, and an optional list of branches `branches`. If `branches` isn't given, the constructor uses the empty list `[]` as the default.
- The `label` selector returns the value of the root, while the `branches` selector returns the list of branches of the tree.

With this in mind, we can create the tree from earlier using our constructor:

```
t = tree(1,
      [tree(3,
          [tree(4),
           tree(5),
           tree(6)]),
      tree(2)])
```