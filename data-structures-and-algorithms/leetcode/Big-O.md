# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Big O](#big-o)
  - [How complexity works](#how-complexity-works)

## Big O

Big O is a notation used to describe the "computational complexity" of an algorithm. The computational complexity of an algorithm is split into two parts: time complexity and space complexity. The time complexity of an algorithm is the amount of time the algorithm needs to run relative to the input size. The space complexity of an algorithm is the amount of memory used by the algorithm relative to the input size.

- **Time complexity**: as the input size grows, how much longer does the algorithm take to complete?
- **Space complexity**: as the input size grows, how much more memory does the algorithm use?

## How complexity works

Complexity is described by a function (math formula). What should the variables in this function be?

The variables are defined by you, but they should represent values that change between different inputs, and these values should affect the algorithm. For example, the most common variable you'll see is ***n***, which usually denotes the length of an input array or string. In the example above, we could say that ***n*** is equal to the length of `nums`.

Here, "the length of `nums`" is a value that changes between inputs, and it directly affects the algorithm. The longer `nums` is, the more elements we need to iterate through, and thus the longer our algorithm will take to complete.

When written, the function is wrapped by a capital O. Here are some example complexities:

- $O(n)$
- $O(n^2)$
- $O(2^n)$
- $O(logn)$
- $O(n⋅m)$

These functions represent the complexity. For example, you would say "The time complexity of my algorithm is $O(n)$" or "The space complexity of my algorithm is $O(n^2)$".