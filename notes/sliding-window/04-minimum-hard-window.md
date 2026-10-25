# Level 4 — Minimum / hard window

**Topic status: Fully Completed (user-confirmed).** Per-problem labels below preserve the provided historical distinctions.

## Problems and recognition

| Problem | Historical status | Recognition / intuition |
|---|---|---|
| [LC 76 — Minimum Window Substring](https://leetcode.com/problemset/?search=76) | Covered; track complete | Find the shortest window satisfying required character counts, including multiplicities. |

## What to learn

- Keep a need/frequency map.
- Expand until all character requirements are met.
- Shrink greedily while still valid, recording a best candidate.
- The answer is minimum valid length, unlike usual maximum-window problems.

## Typical complexity

A standard two-pointer window traverses the input in **O(n)** time with **O(1)** auxiliary space for sum/count-only constraints. Character maps usually use **O(Σ)** space for alphabet size Σ; index deques or prefix arrays can take **O(n)**. Problem-specific constraints, such as multiple passes, may change constants but not the asymptotic bounds.

## Common mistakes

Counting unique distinct characters is insufficient when the target contains duplicates. A required/formed invariant or a deficit counter must track exact multiplicities.

## Implementation and revision checklist

1. Write a brute-force baseline and characterize valid windows.
2. State the window invariant, and decide whether to shrink before or after recording an answer.
3. Implement independently in Python and test edge cases, including zeros, repeated values, and small arrays.
4. Explain why each element enters/leaves the window or deque a bounded number of times.

> Curated explanations, not verbatim chat exports or your saved accepted code. The level's inclusion in the completed track does not independently verify every submitted solution.
