# Level 2 — Variable-size window

**Topic status: Fully Completed (user-confirmed).** Per-problem labels below preserve the provided historical distinctions.

## Problems and recognition

| Problem | Historical status | Recognition / intuition |
|---|---|---|
| [LC 209 — Minimum Size Subarray Sum](https://leetcode.com/problemset/?search=209) | Solved | Accumulate positive values and shrink while sum >= target to minimize length. |
| [LC 3 — Longest Substring Without Repeating Characters](https://leetcode.com/problemset/?search=3) | Solved / Introduced | Remove duplicates before or after including right character depending on the invariant. |
| [LC 904 — Fruit Into Baskets](https://leetcode.com/problemset/?search=904) | Covered; track complete | Maintain at most 2 distinct fruit types. |
| [LC 1004 — Max Consecutive Ones III](https://leetcode.com/problemset/?search=1004) | Covered; track complete | Maintain at most k zeros. |
| [LC 424 — Longest Repeating Character Replacement](https://leetcode.com/problemset/?search=424) | Covered; track complete | Keep window where length - max_character_frequency <= k. |

## What to learn

- Expand with right pointer; shrink from left when the relevant condition is violated or when optimizing a minimum.
- Distinguish minimum valid window from maximum valid window.
- Use a set or frequency map for distinctness, and a scalar for count constraints.
- The invariant depends on the problem; not every sliding window has identical update order.

## Typical complexity

A standard two-pointer window traverses the input in **O(n)** time with **O(1)** auxiliary space for sum/count-only constraints. Character maps usually use **O(Σ)** space for alphabet size Σ; index deques or prefix arrays can take **O(n)**. Problem-specific constraints, such as multiple passes, may change constants but not the asymptotic bounds.

## Common mistakes

LC 209 uses a strictly positive input assumption for monotonic shrinking. LC 3 requires valid unique characters before measuring the current candidate; LC 424 can use a historical maximum frequency.

## Implementation and revision checklist

1. Write a brute-force baseline and characterize valid windows.
2. State the window invariant, and decide whether to shrink before or after recording an answer.
3. Implement independently in Python and test edge cases, including zeros, repeated values, and small arrays.
4. Explain why each element enters/leaves the window or deque a bounded number of times.

> Curated explanations, not verbatim chat exports or your saved accepted code. The level's inclusion in the completed track does not independently verify every submitted solution.


## Python reference implementations

### LC 209 — Minimum Size Subarray Sum
```python
class Solution:
    def minSubArrayLen(self, target, nums):
        left = total = 0
        best = len(nums) + 1
        for right, value in enumerate(nums):
            total += value
            while total >= target:
                best = min(best, right - left + 1)
                total -= nums[left]
                left += 1
        return 0 if best == len(nums) + 1 else best
```
### LC 3 — Longest Substring Without Repeating Characters
```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        seen = set()
        left = best = 0
        for right, char in enumerate(s):
            while char in seen:
                seen.remove(s[left])
                left += 1
            seen.add(char)
            best = max(best, right - left + 1)
        return best
```
### LC 904 — Fruit Into Baskets
```python
from collections import defaultdict
class Solution:
    def totalFruit(self, fruits):
        counts = defaultdict(int)
        left = best = 0
        for right, fruit in enumerate(fruits):
            counts[fruit] += 1
            while len(counts) > 2:
                old = fruits[left]
                counts[old] -= 1
                if counts[old] == 0: del counts[old]
                left += 1
            best = max(best, right-left+1)
        return best
```
### LC 1004 — Max Consecutive Ones III
```python
class Solution:
    def longestOnes(self, nums, k):
        left = zeros = best = 0
        for right, value in enumerate(nums):
            if value == 0: zeros += 1
            while zeros > k:
                if nums[left] == 0: zeros -= 1
                left += 1
            best = max(best, right-left+1)
        return best
```
### LC 424 — Longest Repeating Character Replacement
```python
from collections import defaultdict
class Solution:
    def characterReplacement(self, s, k):
        counts = defaultdict(int)
        left = best = max_freq = 0
        for right, char in enumerate(s):
            counts[char] += 1
            max_freq = max(max_freq, counts[char])
            while right-left+1-max_freq > k:
                counts[s[left]] -= 1
                left += 1
            best = max(best, right-left+1)
        return best
```
