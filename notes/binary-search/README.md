# Binary Search — Level-by-level roadmap

**Current progress:** Levels 1–3 completed.

| Level | Pattern | Problems | Guide |
|---|---|---|---|
| 1 | Classical Binary Search | 704, 35, 69, 367 | [Level 1](01-classical.md) |
| 2 | Boundaries and Insertion Positions | 34, 278, 744, 1539 | [Level 2](02-boundaries.md) |
| 3 | Rotated Sorted Arrays | 33, 81, 153, 154 | [Level 3](03-rotated-arrays.md) |

## Recognition
- **Exact element:** standard left/right binary search.
- **First/last occurrence, insertion location:** lower/upper bounds and monotonic predicates.
- **Rotated sorted array:** use the sorted half or locate pivot using the rightmost value.
- **Duplicates in rotated arrays:** when equality blocks direction, shrink the boundary carefully.

These guides contain reconstructed Python reference implementations, not the learner's historical accepted submissions.
