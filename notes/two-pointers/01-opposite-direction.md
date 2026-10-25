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
