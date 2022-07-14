#### Binary numbers

```pseudocode
0110 (base 2)
0x23 + 1x22 + 1x21 + 0x20
```



```pseudocode
000   0
001   1
010   2
011   3
100   4
101   5
110   6
111   7

max value = 2^3 -1
```

#### Signed negative numbers



##### Negative - two's complement

1. start with an unsigned 4-bit binary number where leftmost bit is 0
   * 0110 = 6

2. complement your binary number (flip bits)
   * 1001
3.  add one to your binary number
   * 1010 = -6



* n-bit *signed* binary numbers: $-2^{n-1}... 2^{n-1}-1$
* Summing signed binary number is easy



#### Boolean logic

**a** *and* **b**

| **a** | **b** | **a** *and* **b** |
| ----- | ----- | ----------------- |
| 1     | 1     | 1                 |
| 1     | 0     | 0                 |
| 0     | 1     | 0                 |
| 0     | 0     | 0                 |



**a** *or* **b**

| **a** | **b** | **a** *or* **b** |
| ----- | ----- | ---------------- |
| 1     | 1     | 1                |
| 1     | 0     | 1                |
| 0     | 1     | 1                |
| 0     | 0     | 0                |

*not* **a**

| **a** | *not* **a** |
| ----- | ----------- |
| 1     | 0           |
| 0     | 1           |



#### Circuits