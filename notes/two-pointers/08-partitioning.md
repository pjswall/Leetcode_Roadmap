# Level 8 — Partitioning variants

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 75 — Sort Colors](https://leetcode.com/problems/sort-colors/) | Dutch national flag: low, mid, high regions. | O(n) | O(1) |
| [LC 86 — Partition List](https://leetcode.com/problems/partition-list/) | Build stable before/after chains and reconnect safely. | O(n) | O(1) |
| [LC 905 — Sort Array By Parity](https://leetcode.com/problems/sort-array-by-parity/) | Move even values to one side using opposite pointers. | O(n) | O(1) |
| [LC 922 — Sort Array By Parity II](https://leetcode.com/problems/sort-array-by-parity-ii/) | Use even/odd index pointers in increments of 2, swapping misplaced values. | O(n) | O(1) |

## What this level teaches

- Three-way partition
- Stable partition
- Binary partition
- Index-based partition

## Core technique

Maintain explicit partitions or index classes. A swap either fixes a segment or moves an unprocessed item into a position requiring another check.

## Common mistakes and boundary cases

After swapping with an unprocessed high region in LC 75, recheck the current index; LC 86 must terminate the after-chain; LC 922 is marked Current only in the historical snapshot provided, while the topic is confirmed complete.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.
