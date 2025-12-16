# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Two pointers](#two-pointers)
    - [Example 1](#example-1)
    - [Example 2](#example-2)
  - [Another way to use two pointers](#another-way-to-use-two-pointers)
    - [Example 3](#example-3)
    - [Example 4](#example-4)

## Two pointers

Two pointers is an extremely common technique used to solve array and string problems. It involves having two integer variables that both move along an iterable. In this article, we are focusing on arrays and strings. This means we will have two integers, usually named something like `i` and `j`, or `left` and `right` which each represent an index of the array or string.

There are several ways to implement two pointers. To start, let's look at the following method:

> Start the pointers at the edges of the input. Move them towards each other until they meet.

Converting this idea into instructions:

1. Start one pointer at the first index 0 and the other pointer at the last index input.length - 1.
1. Use a while loop until the pointers are equal to each other.
1. At each iteration of the loop, move the pointers towards each other. This means either increment the pointer that started at the first index, decrement the pointer that started at the last index, or both. Deciding which pointers to move will depend on the problem we are trying to solve.

Here's some pseudocode illustrating the concept:

```
function fn(arr):
    left = 0
    right = arr.length - 1

    while left < right:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. left++
            2. right--
            3. Both left++ and right--
```

The strength of this technique is that we will never have more than $O(n)$ iterations for the while loop because the pointers start $n$ away from each other and move at least one step closer in every iteration. Therefore, if we can keep the work inside each iteration at $O(1)$, this technique will result in a linear runtime, which is usually the best possible runtime. Let's look at some examples.

### Example 1

>  Given a string `s`, return `true` if it is a palindrome, `false` otherwise. A string is a palindrome if it reads the same forward as backward. That means, after reversing it, it is still the same string. For example: "abcdcba", or "racecar".

After reversing a string, the first character becomes the last character. If a string is the same after being reversed, that means the first character is the same as the last character, the second character is the same as the second last character, and so on. We can use the two pointers technique here to check that all corresponding characters are equal. To start, we check the first and last characters using two separate pointers. To check the next pair of characters, we just need to move our pointers toward each other one position. We continue until the pointers meet each other or we find a mismatch.

```python
def check_if_palindrome(s):
    left = 0
    right = len(s) - 1

    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    
    return True
```

Notice that if the input was an array of characters instead of a string, the algorithm wouldn't change. The two pointers technique works as long as the index variables are moving along some abstract iterable.

This algorithm is very efficient as not only does it run in $O(n)$, but it also uses only $O(1)$ space. No matter how big the input is, we always only use two integer variables. The time complexity is $O(n)$ because the while loop iterations cost $O(1)$ each, and there can never be more than $O(n)$ iterations of the while loop - the pointers start at a distance of $n$ from each other and move closer by one step each iteration.

### Example 2

>  Given a **sorted** array of unique integers and a target integer, return `true` if there exists a pair of numbers that sum to target, `false` otherwise. For example, given `nums = [1, 2, 4, 6, 8, 9, 14, 15]` and `target = 13`, return true because `4 + 9 = 13`.

The brute force solution would be to iterate over all pairs of integers. Each number in the array can be paired with another number, so this would result in a time complexity of $O(n^2)$, where $n$ is the length of the array. Because the array is sorted, we can use two pointers to improve to an $O(n)$ time complexity.

Let's use the example input. With two pointers, we start by looking at the first and last numbers. Their sum is `1 + 15 = 16`. Because `16 > target`, we need to make our current sum smaller. Therefore, we should move the `right` pointer. Now, we have `1 + 14 = 15`. Again, move the right pointer because the sum is too large. Now, `1 + 9 = 10`. Since the sum is too small, we need to make it bigger, which can be done by moving the `left` pointer. `2 + 9 = 11 < target`, so move it again. Finally, `4 + 9 = 13 = target`.

The reason this algorithm works: because the numbers are sorted, moving the left pointer permanently increases the value the left pointer points to (`nums[left] = x`). Similarly, moving the right pointer permanently decreases the value the right pointer points to (`nums[right] = y`). If we have `x + y > target`, then we can never have a solution with `y` because `x` can only increase. So if a solution exists, we can only find it by decreasing `y`. The same logic can be applied to x if `x + y < target`.

```python
def check_for_target(nums, target):
    left = 0
    right = len(nums) - 1

    while left < right:
        # curr is the current sum
        curr = nums[left] + nums[right]
        if curr == target:
            return True
        if curr > target:
            right -= 1
        else:
            left += 1
    
    return False
```

Like in the previous example, this algorithm uses $O(1)$ space and has a time complexity of $O(n)$.

## Another way to use two pointers

This method where we start the pointers at the first and last indices and move them towards each other is only one way to implement two pointers. Algorithms are beautiful because of how abstract they are - "two pointers" is just an idea, and it can be implemented in many different ways. Let's look at another method and some new examples. The following method is applicable when the problem has two iterables in the input, for example, two arrays.

> Move along both inputs simultaneously until all elements have been checked.

Converting this idea into instructions:

1. Create two pointers, one for each iterable. Each pointer should start at the first index.
1. Use a while loop until one of the pointers reaches the end of its iterable.
1. At each iteration of the loop, move the pointers forward. This means incrementing either one of the pointers or both of the pointers. Deciding which pointers to move will depend on the problem we are trying to solve.
1. Because our while loop will stop when one of the pointers reaches the end, the other pointer will not be at the end of its respective iterable when the loop finishes. Sometimes, we need to iterate through all elements - if this is the case, you will need to write extra code here to make sure both iterables are exhausted.

Here's some pseudocode illustrating the concept:

```
function fn(arr1, arr2):
    i = j = 0
    while i < arr1.length AND j < arr2.length:
        Do some logic here depending on the problem
        Do some more logic here to decide on one of the following:
            1. i++
            2. j++
            3. Both i++ and j++

    // Step 4: make sure both iterables are exhausted
    // Note that only one of these loops would run
    while i < arr1.length:
        Do some logic here depending on the problem
        i++

    while j < arr2.length:
        Do some logic here depending on the problem
        j++
```

Similar to the first method we looked at, this method will have a linear time complexity of $O(n+m)$ if the work inside the while loop is $O(1)$, where `n = arr1.length` and `m = arr2.length`. This is because at every iteration, we move at least one pointer forward, and the pointers cannot be moved forward more than `n + m` times without the arrays being exhausted.

### Example 3

> Given two sorted integer arrays arr1 and arr2, return a new array that combines both of them and is also sorted.

The trivial approach would be to first combine both input arrays and then perform a sort. If we have `n = arr1.length + arr2.length`, then this gives a time complexity of $O(n⋅logn)$ (the cost of sorting). This would be a good approach if the input arrays were not sorted, but because they are sorted, we can take advantage of the two pointers technique to improve to $O(n)$.

> In the previous example, we declared `n = arr1.length` and `m = arr2.length`. Here, we are saying `n = arr1.length + arr2.length`. Why have we changed the definition? Remember that when it comes to big O, **we are allowed to define the variables as we see fit**. We could certainly stick to using `n`, `m`. In that case, the time complexity of the sorting approach would be $O((n+m)⋅log(m+n))$ and the time complexity of the approach we are about to cover would be 
$O(n+m)$. It makes no difference either way, but one justification we could give here is that since we are combining the arrays, the total length is a significant number, so it makes sense to represent it as `n`. Keeping the definition as `n = arr1.length` and `m = arr2.length` is fine as well.

We can build the answer array `ans` one element at a time. Start two pointers at the first index of each array, and compare their elements. At each iteration, we have 2 values. Whichever value is lower needs to come first in the answer, so add it to the answer and move the respective pointer.

```python
def combine(arr1, arr2):
    # ans is the answer
    ans = []
    i = j = 0
    while i < len(arr1) and j < len(arr2):
        if arr1[i] < arr2[j]:
            ans.append(arr1[i])
            i += 1
        else:
            ans.append(arr2[j])
            j += 1
    
    while i < len(arr1):
        ans.append(arr1[i])
        i += 1
    
    while j < len(arr2):
        ans.append(arr2[j])
        j += 1
    
    return ans
```

Like in the previous two examples, this algorithm has a time complexity of $O(n)$ and uses 
$O(1)$ space (if we don't count the output as extra space, which we usually don't).

### Example 4

> Given two strings `s` and `t`, return `true` if `s` is a subsequence of `t`, or `false` otherwise. A subsequence of a string is a sequence of characters that can be obtained by deleting some (or none) of the characters from the original string, while maintaining the relative order of the remaining characters. For example, "ace" is a subsequence of "abcde" while "aec" is not.

We can use two pointers to solve this in linear time. If we find that `s[i] == t[j]`, that means we "found" the letter at position `i` for `s`, and we can move on to the next one by incrementing `i`. We should increment `j` at each iteration no matter what (which means we could also implement this algorithm using a for loop). `s` is a subsequence of `t` if we can "find" all the letters of `s`, which means that `i == s.length` at the end of the algorithm.

```python
class Solution:
    def isSubsequence(self, s: str, t: str) -> bool:
        i = j = 0
        while i < len(s) and j < len(t):
            if s[i] == t[j]:
                i += 1
            j += 1

        return i == len(s)
```

Just like all the prior examples, this solution uses ; space. The time complexity is linear with the lengths of `s` and `t`.