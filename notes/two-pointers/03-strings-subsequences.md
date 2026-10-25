# Level 3 — String and subsequence pointers

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 392 — Is Subsequence](https://leetcode.com/problems/is-subsequence/) | Advance the subsequence pointer only on a matching character. | O(n+m) | O(1) |
| [LC 844 — Backspace String Compare](https://leetcode.com/problems/backspace-string-compare/) | Traverse backward using skip counters to compare visible characters. | O(n+m) | O(1) |
| [LC 925 — Long Pressed Name](https://leetcode.com/problems/long-pressed-name/) | Allow repeated typed characters only when they match the preceding character. | O(n+m) | O(1) |
| [LC 680 — Valid Palindrome II](https://leetcode.com/problems/valid-palindrome-ii/) | On first mismatch, try skipping either the left or right character once. | O(n) | O(1) |

## What this level teaches

- One pointer per string
- Conditional pointer movement
- Skipping characters
- Allowing one mismatch

## Core technique

Different streams move at different rates. Every pointer advance needs to represent consuming an actual character (or a deliberate skip).

## Common mistakes and boundary cases

Do not advance both pointers unconditionally. LC 680 must try both deletion alternatives.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.


## Python reference implementations

### LC 392 — Is Subsequence
```python
class Solution:
    def isSubsequence(self, s, t):
        i = 0
        for char in t:
            if i < len(s) and char == s[i]:
                i += 1
        return i == len(s)
```
### LC 844 — Backspace String Compare
```python
class Solution:
    def backspaceCompare(self, s, t):
        def visible(text):
            i, skip = len(text) - 1, 0
            while i >= 0:
                if text[i] == "#": skip += 1
                elif skip: skip -= 1
                else: yield text[i]
                i -= 1
        from itertools import zip_longest
        return all(a == b for a, b in zip_longest(visible(s), visible(t)))
```
### LC 925 — Long Pressed Name
```python
class Solution:
    def isLongPressedName(self, name, typed):
        i = 0
        for j, char in enumerate(typed):
            if i < len(name) and char == name[i]:
                i += 1
            elif j == 0 or char != typed[j - 1]:
                return False
        return i == len(name)
```
### LC 680 — Valid Palindrome II
```python
class Solution:
    def validPalindrome(self, s):
        def check(l, r):
            while l < r:
                if s[l] != s[r]: return False
                l += 1
                r -= 1
            return True
        l, r = 0, len(s) - 1
        while l < r:
            if s[l] != s[r]:
                return check(l + 1, r) or check(l, r - 1)
            l += 1
            r -= 1
        return True
```
