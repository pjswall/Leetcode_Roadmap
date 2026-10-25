# Level 6 — Two sorted collections and intervals

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 88 — Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) | Merge from the back to avoid overwriting unread nums1 values. | O(m+n) | O(1) |
| [LC 986 — Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/) | Take max starts and min ends; advance the interval ending first. | O(m+n) | O(1) excluding output |
| [LC 350 — Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/) | Sort both arrays; record an equal value, advancing both pointers. | O(m log m+n log n) | O(1) scan excluding output/sort |
| [LC 658 — Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/) | After sorting, shrink a candidate range until exactly k elements remain. | O(n-k) for shrink on sorted input | O(1) extra excluding output |

## What this level teaches

- One pointer per collection
- Comparing current values
- Advancing only the relevant pointer
- Interval overlap logic

## Core technique

Use ordered inputs to avoid restarting scans. Compare current elements, take a useful action, then advance only pointers whose value or interval is no longer relevant.

## Common mistakes and boundary cases

LC 350's multiplicities matter; LC 986's overlap boundary is inclusive; LC 658 also admits binary search for left boundary.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.
