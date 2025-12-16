# Table of Contents
- [Table of Contents](#table-of-contents)
  - [More common patterns](#more-common-patterns)
    - [O(n) string building](#on-string-building)
    - [Subarrays/substrings, subsequences, and subsets](#subarrayssubstrings-subsequences-and-subsets)

## More common patterns

In this article, we'll briefly talk about a few more patterns and some common tricks that can be used in algorithm problems regarding arrays and strings.

### O(n) string building

We mentioned earlier that in most languages, strings are immutable. This means concatenating a single character to a string is an $O(n)$ operation. If you have a string that is 1 million characters long, and you want to add one more character, all 1 million characters need to be copied over to another string.

Many problems will ask you to return a string, and usually, this string will be built during the algorithm. Let's say the final string is of length `n` and we build it one character at a time with concatenation. What would the time complexity be? The operations needed at each step would be `1 + 2 + 3 + ... + n`. This is the partial sum of [this series](https://en.wikipedia.org/wiki/1_%2B_2_%2B_3_%2B_4_%2B_%E2%8B%AF#Partial_sums), which leads to $O(n^2)$ operations.

Simple concatenation will result in an $O(n^2)$ time complexity if you are using a language where strings are immutable.

There are better ways to build strings in just $O(n)$ time. This will vary between languages - here, we'll talk about Python - if you're using another language, we recommend researching the best way to build strings in your language.

- Declare a list
- When building the string, add the characters to the list. This is $O(1)$ per operation. Across n operations, it will cost $O(n)$ in total.
- Once finished, convert the list to a string using "".join(list). This is $O(n)$. 
- In total, it cost us $O(n+n)=O(2n)=O(n)$.

```
def build_string(s):
    arr = []
    for c in s:
        arr.append(c)

    return "".join(arr)
```

### Subarrays/substrings, subsequences, and subsets

Let's quickly talk about the differences between these words and what to look out for when encountering them in problems.

**Subarrays/substrings**

> As a reminder, a subarray or substring is a contiguous section of an array or string.

**Subsequences**

> A subsequence is a set of elements of an array/string that keeps the same relative order but doesn't need to be contiguous. For example, subsequences of `[1, 2, 3, 4]` include: `[1, 3]`, `[4]`, `[]`, `[2, 3]`, but not `[3, 2]`, `[5]`, `[4, 1]`.

**Subsets**

> A subset is any set of elements from the original array or string. The order doesn't matter and the elements don't need to be beside each other. For example, given `[1, 2, 3, 4]`, all of these are subsets: `[3, 2]`, `[4, 1, 2]`, `[1]`. Note: subsets that contain the same elements are usually considered the same, so `[1, 2, 4]` is the same subset as `[4, 1, 2]`.