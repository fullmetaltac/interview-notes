## Maximum Number of Balloons

Given a string `text`, you want to use the characters of `text` to form as many instances of the word **"balloon"** as possible.

You can use each character in `text` **at most once**. Return the maximum number of instances that can be formed.

**Example 1:**

```
Input: text = "nlaebolko"
Output: 1
```

**Example 2:**

```
Input: text = "loonbalxballpoon"
Output: 2
```

**Example 3:**

```
Input: text = "leetcode"
Output: 0
```
 

**Constraints:**

- `1 <= text.length <= 104`
- text consists of lower case English letters only.

```python
class Solution:
    def maxNumberOfBalloons(self, text: str) -> int:
        pattern_str = "balloon"
        pattern_elem_freq = Counter(pattern_str)
        text_elem_freq = Counter(text)
        max_pattern_count = math.inf

        for char in pattern_str:
            freq = text_elem_freq[char] // pattern_elem_freq[char]
            max_pattern_count = min(max_pattern_count, freq)
        return max_pattern_count
```