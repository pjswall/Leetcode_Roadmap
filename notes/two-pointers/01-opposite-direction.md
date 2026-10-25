# Level 1 — Opposite-direction pointers

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 125 — Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) | Skip non-alphanumeric symbols; compare lowercased endpoints. | O(n) | O(1) |
| [LC 344 — Reverse String](https://leetcode.com/problems/reverse-string/) | Swap left and right characters in place. | O(n) | O(1) |
| [LC 167 — Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) | Use sorted order: small sum -> move left; large sum -> move right. | O(n) | O(1) |
| [LC 977 — Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/) | Place larger-magnitude square at the back of output. | O(n) | O(n) |

## What this level teaches

- left < right
- Moving both ends inward
- Skipping unwanted values
- Using sorted order

## Core technique

Start with opposite ends. Base movement on the invariant: characters can be skipped; sorted data tells which side can be discarded.

## Common mistakes and boundary cases

Strict pointer bounds; compare values after skipping; remember LC 167 returns 1-indexed answers.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.


## Python reference implementations

### LC 125 — Valid Palindrome
```python
class Solution:
    def isPalindrome(self, s):
        left, right = 0, len(s) - 1
        while left < right:
            while left < right and not s[left].isalnum(): left += 1
            while left < right and not s[right].isalnum(): right -= 1
            if s[left].lower() != s[right].lower(): return False
            left += 1
            right -= 1
        return True
```
### LC 344 — Reverse String
```python
class Solution:
    def reverseString(self, s):
        left, right = 0, len(s) - 1
        while left < right:
            s[left], s[right] = s[right], s[left]
            left += 1
            right -= 1
```
### LC 167 — Two Sum II
```python
class Solution:
    def twoSum(self, numbers, target):
        l, r = 0, len(numbers) - 1
        while l < r:
            total = numbers[l] + numbers[r]
            if total == target: return [l + 1, r + 1]
            if total < target: l += 1
            else: r -= 1
```
### LC 977 — Squares of a Sorted Array
```python
class Solution:
    def sortedSquares(self, nums):
        l, r, pos = 0, len(nums) - 1, len(nums) - 1
        ans = [0] * len(nums)
        while l <= r:
            if abs(nums[l]) > abs(nums[r]):
                ans[pos] = nums[l] ** 2
                l += 1
            else:
                ans[pos] = nums[r] ** 2
                r -= 1
            pos -= 1
        return ans
```
