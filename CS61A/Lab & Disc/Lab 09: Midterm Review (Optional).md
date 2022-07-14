# Orders of growth

The order of growth of an algorithm is an approximation of the time required to run a computer program as the input size increases. The order of growth ignores the constant factor needed for fixed operations and focuses instead on the operations that increase proportional to input size. For example, a program with a linear order of growth generally requires double the time if the input doubles.

The order of growth is often described using either [Big-Theta](https://www.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/big-big-theta-notation) or [Big-O notation](https://www.khanacademy.org/computing/computer-science/algorithms/asymptotic-notation/a/big-o-notation), but that notation is out of scope for this course.

This table summarizes the most common orders of growth:

| Order       | Big-Theta | Example                                |
| :---------- | :-------- | :------------------------------------- |
| Constant    | Θ(1)      | Indexing an item in a list             |
| Logarithmic | Θ(lg N)   | Repeatedly halving a number            |
| Linear      | Θ(n)      | Summing a list                         |
| Quadratic   | Θ(n^2)    | Summing each pair of numbers in a list |
| Exponential | Θ(2^n)    | Visiting each node in a binary tree    |