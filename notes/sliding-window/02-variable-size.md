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
