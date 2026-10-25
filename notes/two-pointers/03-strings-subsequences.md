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
