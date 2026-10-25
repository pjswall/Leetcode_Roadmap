# Level 7 — Fast and slow pointers

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 141 — Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) | Move slow by one and fast by two; meeting implies a cycle. | O(n) | O(1) |
| [LC 142 — Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) | After the pointers meet, reset one to head and advance both to cycle entry. | O(n) | O(1) |
| [LC 876 — Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) | Move fast twice as quickly; slow reaches middle (second middle if even). | O(n) | O(1) |
| [LC 202 — Happy Number](https://leetcode.com/problems/happy-number/) | Treat digit-square-sum sequence as a functional graph; cycle detects non-happy. | O(log n) per transition | O(1) |
| [LC 287 — Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/) | Treat each value as a next-index pointer; Floyd cycle entry yields duplicate. | O(n) | O(1) |

## What this level teaches

- Tortoise-and-hare technique
- Detecting cycles
- Finding cycle entry points
- Applying linked-list logic to arrays and numbers

## Core technique

Model links or deterministic next-state functions as a graph. A fast pointer eventually meets a slow pointer in a cycle; a second phase can locate entry.

## Common mistakes and boundary cases

Check fast and fast.next before a two-step advance; distinguish collision detection from cycle-entry recovery.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.
