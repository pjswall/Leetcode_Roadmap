# Level 1 — Fixed-size window

**Topic status: Fully Completed (user-confirmed).** Per-problem labels below preserve the provided historical distinctions.

## Problems and recognition

| Problem | Historical status | Recognition / intuition |
|---|---|---|
| [LC 643 — Maximum Average Subarray I](https://leetcode.com/problemset/?search=643) | Solved | Track sum of k values; subtract the outgoing element. |
| [LC 1456 — Maximum Number of Vowels in a Substring of Given Length](https://leetcode.com/problemset/?search=1456) | Solved | Count vowels in each length-k window. |
| [LC 1343 — Number of Sub-arrays of Size K and Average Greater than or Equal to Threshold](https://leetcode.com/problemset/?search=1343) | Solved | Compare window sum to k*threshold to avoid floating-point issues. |
| [LC 2379 — Minimum Recolors to Get K Consecutive Black Blocks](https://leetcode.com/problemset/?search=2379) | Solved | Minimize white blocks in each window of length k. |

## What to learn

- A fixed window always holds exactly k elements.
- Initialize the first window; each slide adds one value and removes one.
- Compute the answer for all n-k+1 windows.
- Sliding window sum vs prefix sum: prefix[right] - prefix[left] for half-open ranges.

## Typical complexity

A standard two-pointer window traverses the input in **O(n)** time with **O(1)** auxiliary space for sum/count-only constraints. Character maps usually use **O(Σ)** space for alphabet size Σ; index deques or prefix arrays can take **O(n)**. Problem-specific constraints, such as multiple passes, may change constants but not the asymptotic bounds.

## Common mistakes

Off-by-one: after processing the first k elements, the next incoming index is k. Prefix arrays of length n+1 start with a zero and make [left,right) subtraction natural.

## Implementation and revision checklist

1. Write a brute-force baseline and characterize valid windows.
2. State the window invariant, and decide whether to shrink before or after recording an answer.
3. Implement independently in Python and test edge cases, including zeros, repeated values, and small arrays.
4. Explain why each element enters/leaves the window or deque a bounded number of times.

> Curated explanations, not verbatim chat exports or your saved accepted code. The level's inclusion in the completed track does not independently verify every submitted solution.


## Python reference implementations

### LC 643 — Maximum Average Subarray I
```python
class Solution:
    def findMaxAverage(self, nums, k):
        window = sum(nums[:k])
        best = window
        for right in range(k, len(nums)):
            window += nums[right] - nums[right - k]
            best = max(best, window)
        return best / k
```
### LC 1456 — Maximum Number of Vowels
```python
class Solution:
    def maxVowels(self, s, k):
        vowels = set("aeiou")
        count = sum(ch in vowels for ch in s[:k])
        best = count
        for right in range(k, len(s)):
            count += (s[right] in vowels) - (s[right-k] in vowels)
            best = max(best, count)
        return best
```
### LC 1343 — Sub-arrays of Size K and Average >= Threshold
```python
class Solution:
    def numOfSubarrays(self, arr, k, threshold):
        window = sum(arr[:k])
        target = k * threshold
        answer = int(window >= target)
        for right in range(k, len(arr)):
            window += arr[right] - arr[right-k]
            answer += window >= target
        return answer
```
### LC 2379 — Minimum Recolors
```python
class Solution:
    def minimumRecolors(self, blocks, k):
        white = blocks[:k].count("W")
        best = white
        for right in range(k, len(blocks)):
            white += (blocks[right] == "W") - (blocks[right-k] == "W")
            best = min(best, white)
        return best
```
