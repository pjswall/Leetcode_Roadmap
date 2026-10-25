# Level 4 — Anchor plus two pointers

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 15 — 3Sum](https://leetcode.com/problems/3sum/) | Sort, fix an anchor, search opposing ends; skip duplicate triplets. | O(n²) | O(1) extra, excluding output/sort |
| [LC 16 — 3Sum Closest](https://leetcode.com/problems/3sum-closest/) | Keep nearest encountered total while moving pointers by sum comparison. | O(n²) | O(1) extra |
| [LC 18 — 4Sum](https://leetcode.com/problems/4sum/) | Fix two anchors, two-pointer scan the remaining sorted range. | O(n³) | O(1) extra, excluding output/sort |
| [LC 259 — 3Sum Smaller](https://leetcode.com/problems/3sum-smaller/) | When sum is below target, bulk-count right-left valid pairs for anchor. | O(n²) | O(1) extra |

## What this level teaches

- Sorting first
- Fixing one element
- Searching the remaining range
- Duplicate handling

## Core technique

Sorting converts search for a pair under a fixed anchor to a linear opposing-pointer sweep. Separate uniqueness constraints from counting constraints.

## Common mistakes and boundary cases

In counting problems, bulk-count valid ranges; in unique tuple output problems, skip duplicate anchors and duplicates after a match.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.
