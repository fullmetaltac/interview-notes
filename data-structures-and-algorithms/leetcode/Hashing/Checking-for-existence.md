# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Checking for existence](#checking-for-existence)

## Checking for existence

One of the most common applications of a hash map or set is determining if an element exists in $O(1)$. Since an array needs $O(n)$ to do this, using a hash map or set can improve the time complexity of an algorithm greatly, usually from $O(n^2)$ to $O(n)$. Let's look at some example problems.

**Example 1**
[1. Two Sum](https://leetcode.com/problems/two-sum/)

> Given an array of integers `nums` and an integer `target`, return indices of two numbers such that they add up to `target`. You cannot use the same index twice.

Let's quickly think about how we could solve this problem with a brute force approach. We could simply check every pair of numbers and see if they add up to `target`. Use one for loop to iterate over the array and at each iteration, lock in a number num. Then use an inner for loop which looks for `target - num` in the array (because `num + target - num = target`).

This algorithm is slow because the inner loop (whose purpose is to find `target - num`) costs $O(n)$. Thus, the time complexity would be $O(n^2)$. With a hash map, we can look for `target - num` in $O(1)$, which would greatly improve the time complexity to $O(n)$.

We can build a hash map as we iterate along the array, mapping each value to its index. At each index `i`, where `num = nums[i]`, we can check our hash map for `target - num`. Adding key-value pairs and checking for target - num are all $O(1)$, so our time complexity will improve to $O(n)$.

```python
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        dic = {}
        for i in range(len(nums)):
            num = nums[i]
            complement = target - num
            if complement in dic: # This operation is O(1)!
                return [i, dic[complement]]
            
            dic[num] = i
        
        return [-1, -1]
```

> If the question wanted us to return a boolean indicating if a pair exists or to return the numbers themselves, then we could just use a set. However, since it wants the indices of the numbers, we need to use a hash map to "remember" what indices the numbers are at.

The time complexity is $O(n)$ as the hash map operations are $O(1)$. This solution also uses $O(n)$ space as the number of keys the hash map will store scales linearly with the input size.

**Example 2**

[2351. First Letter to Appear Twice](https://leetcode.com/problems/first-letter-to-appear-twice/)

> Given a string `s`, return the first character to appear twice. It is guaranteed that the input will have a duplicate character.

The brute force solution would be to iterate along the string, and for each character `c`, iterate again up to `c` to see if there is any match.

```python
class Solution:
    def repeatedCharacter(self, s: str) -> str:
        for i in range(len(s)):
            c = s[i]
            for j in range(i):
                if s[j] == c:
                    return c

        return ""
```

This is $O(n^2)$ due to the nested loop. The second loop is checking for the existence of c, which can be done in $O(1)$ using a set.

```python
class Solution:
    def repeatedCharacter(self, s: str) -> str:
        seen = set()
        for c in s:
            if c in seen:
                return c
            seen.add(c)

        return " "
```

This improves our time complexity to $O(n)$ as each for loop iteration now runs in constant time.

The space complexity is a more interesting topic of discussion. Many people will argue that the space complexity is $O(1)$ because the input can only have characters from the English alphabet, which is bounded by a constant (26). This is very common with string problems and technically correct. In an interview setting, this is probably a safe answer, but you should also note that the space complexity could be $O(m)$, where $m$ is the number of allowable characters in the input. This is a more general answer and also technically correct.

**Example 3**

Given an integer array `nums`, find all the numbers `x` in `nums` that satisfy the following:` x + 1` is not in `nums`, and `x - 1` is not in `nums`.

If a valid number `x` appears multiple times, you only need to include it in the answer once.

We can solve this in a straightforward manner - just iterate through `nums` and check if `x + 1` or `x - 1` is in `nums`. By converting `nums` into a set beforehand, these checks will cost $O(1)$.

```python
def find_numbers(nums):
    ans = []
    nums_set = set(nums)

    for num in nums_set:
        if (num + 1 not in nums_set) and (num - 1 not in nums_set):
            ans.append(num)
    
    return ans
```

Because the checks are $O(1)$, the time complexity is $O(n)$ since each for loop iteration runs in constant time. The set will occupy $O(n)$ space.

--- 

Anytime you find your algorithm running `if ... in ...`, then consider using a hash map or set to store elements to have these operations run in $O(1)$. Try these upcoming practice problems with what was learned here.