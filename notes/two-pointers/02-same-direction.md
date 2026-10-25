# Level 2 — Same-direction pointers

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 26 — Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) | Write one instance of each new value. | O(n) | O(1) |
| [LC 27 — Remove Element](https://leetcode.com/problems/remove-element/) | Copy values not equal to the target to write position. | O(n) | O(1) |
| [LC 283 — Move Zeroes](https://leetcode.com/problems/move-zeroes/) | Compact nonzero values preserving their order, then fill zeros. | O(n) | O(1) |
| [LC 80 — Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/) | For each new element, compare with the value two output slots behind. | O(n) | O(1) |

## What this level teaches

- Read pointer and write pointer
- Modifying arrays in place
- Keeping only valid elements
- Avoiding additional arrays

## Core technique

Keep a read pointer scanning input and a write pointer delimiting the valid prefix. Before writing, decide whether the current value belongs in that prefix.

## Common mistakes and boundary cases

The returned length defines the valid prefix, not necessarily the full array contents. LC 80: test write < 2 before accessing write-2.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.
