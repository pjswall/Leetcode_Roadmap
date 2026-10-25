# Level 3 — Frequency matching

**Topic status: Fully Completed (user-confirmed).** Per-problem labels below preserve the provided historical distinctions.

## Problems and recognition

| Problem | Historical status | Recognition / intuition |
|---|---|---|
| [LC 567 — Permutation in String](https://leetcode.com/problemset/?search=567) | Practiced; track complete | Does any fixed-length window have exactly the target character frequencies? |
| [LC 438 — Find All Anagrams in a String](https://leetcode.com/problemset/?search=438) | Solved | Collect starts of every fixed-size window whose character counts equal the pattern. |

## What to learn

- Frequency vectors or hash maps represent character counts.
- A permutation/anagram has the same length as the target pattern.
- For each slide increment incoming and decrement outgoing counts.
- Check equality of frequency distributions or maintain a match counter.

## Typical complexity

A standard two-pointer window traverses the input in **O(n)** time with **O(1)** auxiliary space for sum/count-only constraints. Character maps usually use **O(Σ)** space for alphabet size Σ; index deques or prefix arrays can take **O(n)**. Problem-specific constraints, such as multiple passes, may change constants but not the asymptotic bounds.

## Common mistakes

Do not compare unordered character sets: multiplicities matter. Watch duplicate letters and exact window size.

## Implementation and revision checklist

1. Write a brute-force baseline and characterize valid windows.
2. State the window invariant, and decide whether to shrink before or after recording an answer.
3. Implement independently in Python and test edge cases, including zeros, repeated values, and small arrays.
4. Explain why each element enters/leaves the window or deque a bounded number of times.

> Curated explanations, not verbatim chat exports or your saved accepted code. The level's inclusion in the completed track does not independently verify every submitted solution.
