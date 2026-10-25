# Level 5 — Counting windows

**Topic status: Fully Completed (user-confirmed).** Per-problem labels below preserve the provided historical distinctions.

## Problems and recognition

| Problem | Historical status | Recognition / intuition |
|---|---|---|
| [LC 930 — Binary Subarrays With Sum](https://leetcode.com/problemset/?search=930) | Covered; track complete | Count exact sum via atMost(goal) - atMost(goal-1), or prefix-sum frequency map. |
| [LC 1248 — Count Number of Nice Subarrays](https://leetcode.com/problemset/?search=1248) | Covered; track complete | Count exact k odd numbers using atMost(k)-atMost(k-1). |
| [LC 992 — Subarrays with K Different Integers](https://leetcode.com/problemset/?search=992) | Covered; track complete | Count exactly k distinct values using two at-most windows or subtraction. |

## What to learn

- For nonnegative or suitable monotone constraints, count valid subarrays ending at right in bulk: right-left+1.
- atMost(k) includes all windows with property value <= k; subtraction isolates exactly k.
- Prefix sums + hashmap can count exact sums even when a normal variable-size sliding window is invalid.
- For distinct elements, a frequency dictionary maintains the count of nonzero-frequency keys.

## Typical complexity

A standard two-pointer window traverses the input in **O(n)** time with **O(1)** auxiliary space for sum/count-only constraints. Character maps usually use **O(Σ)** space for alphabet size Σ; index deques or prefix arrays can take **O(n)**. Problem-specific constraints, such as multiple passes, may change constants but not the asymptotic bounds.

## Common mistakes

Never count only one window per right endpoint when many shorter starts also qualify. Handle negative thresholds in atMost helpers. Frequency map initial {0:1} counts subarrays beginning at index zero.

## Implementation and revision checklist

1. Write a brute-force baseline and characterize valid windows.
2. State the window invariant, and decide whether to shrink before or after recording an answer.
3. Implement independently in Python and test edge cases, including zeros, repeated values, and small arrays.
4. Explain why each element enters/leaves the window or deque a bounded number of times.

> Curated explanations, not verbatim chat exports or your saved accepted code. The level's inclusion in the completed track does not independently verify every submitted solution.


## Python reference implementations

### LC 930 — Binary Subarrays With Sum
```python
class Solution:
    def numSubarraysWithSum(self, nums, goal):
        def at_most(limit):
            if limit < 0: return 0
            left = total = count = 0
            for right, value in enumerate(nums):
                total += value
                while total > limit:
                    total -= nums[left]
                    left += 1
                count += right-left+1
            return count
        return at_most(goal)-at_most(goal-1)
```
### LC 1248 — Count Number of Nice Subarrays
```python
class Solution:
    def numberOfSubarrays(self, nums, k):
        def at_most(limit):
            if limit < 0: return 0
            left = odds = count = 0
            for right, value in enumerate(nums):
                odds += value % 2
                while odds > limit:
                    odds -= nums[left] % 2
                    left += 1
                count += right-left+1
            return count
        return at_most(k)-at_most(k-1)
```
### LC 992 — Subarrays With K Different Integers
```python
from collections import defaultdict
class Solution:
    def subarraysWithKDistinct(self, nums, k):
        def at_most(limit):
            if limit < 0: return 0
            freq = defaultdict(int)
            left = count = distinct = 0
            for right, value in enumerate(nums):
                if freq[value] == 0: distinct += 1
                freq[value] += 1
                while distinct > limit:
                    old = nums[left]
                    freq[old] -= 1
                    if freq[old] == 0: distinct -= 1
                    left += 1
                count += right-left+1
            return count
        return at_most(k)-at_most(k-1)
```
