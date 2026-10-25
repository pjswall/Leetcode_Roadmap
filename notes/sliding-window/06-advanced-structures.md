# Level 6 — Advanced structures

**Topic status: Fully Completed (user-confirmed).** Per-problem labels below preserve the provided historical distinctions.

## Problems and recognition

| Problem | Historical status | Recognition / intuition |
|---|---|---|
| [LC 239 — Sliding Window Maximum](https://leetcode.com/problemset/?search=239) | Included in completed track | Monotonic deque of indices, decreasing by value; drop expired front indices. |
| [LC 1696 — Jump Game VI](https://leetcode.com/problemset/?search=1696) | Included in completed track | Deque keeps best DP values over preceding k positions. |
| [LC 1438 — Longest Continuous Subarray With Absolute Diff Less Than or Equal to Limit](https://leetcode.com/problemset/?search=1438) | Included in completed track | Two monotonic deques track current maximum and minimum. |
| [LC 862 — Shortest Subarray with Sum at Least K](https://leetcode.com/problemset/?search=862) | Included in completed track | Prefix sums + increasing deque allow negative numbers and efficient minimum length. |

## What to learn

- A deque stores useful candidate indices, not the entire window.
- Maintain monotonic order, expiring candidates as indices become invalid.
- LC 239, 1696, 1438 combine deque maintenance with windows or DP.
- LC 862 uses prefix sums and a monotonic deque because negative elements break ordinary sliding-window shrinking.

## Typical complexity

A standard two-pointer window traverses the input in **O(n)** time with **O(1)** auxiliary space for sum/count-only constraints. Character maps usually use **O(Σ)** space for alphabet size Σ; index deques or prefix arrays can take **O(n)**. Problem-specific constraints, such as multiple passes, may change constants but not the asymptotic bounds.

## Common mistakes

Store indices to know expiration. Deque is O(n) when each index enters and leaves at most once. Do not mistake LC 862 for a straightforward nonnegative-number sliding window.

## Implementation and revision checklist

1. Write a brute-force baseline and characterize valid windows.
2. State the window invariant, and decide whether to shrink before or after recording an answer.
3. Implement independently in Python and test edge cases, including zeros, repeated values, and small arrays.
4. Explain why each element enters/leaves the window or deque a bounded number of times.

> Curated explanations, not verbatim chat exports or your saved accepted code. The level's inclusion in the completed track does not independently verify every submitted solution.
