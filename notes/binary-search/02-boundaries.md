# Level 2 — Boundaries and Insertion Positions

**Status:** Completed. **Recognition:** find a boundary (first true, first >=, last <=) rather than just any matching index.

| LC | Problem | Key recognition | Complexity |
|---|---|---|---|
| 34 | Find First and Last Position of Element | Two lower bounds: target, target+1 | O(log n), O(1) |
| 278 | First Bad Version | First true in monotone bad-version predicate | O(log n), O(1) |
| 744 | Find Smallest Letter Greater Than Target | Upper bound with cyclic wrap | O(log n), O(1) |
| 1539 | Kth Missing Positive Number | Missing count at i is arr[i]-(i+1) | O(log n), O(1) |

## Invariant and mistakes
With half-open bounds `[left,right)`, `right` may equal n. Predicate binary search keeps the earliest satisfying index inside the candidate interval. LC 744 is **strictly greater**, not greater-or-equal, and wraps to the first letter. In LC 1539, the earliest index with at least k missing numbers determines the answer `left+k`.

## Python reference solutions (reconstructed)

### LC 34
```python
class Solution:
    def searchRange(self, nums, target):
        def lower_bound(value):
            l, r = 0, len(nums)
            while l < r:
                mid = (l + r) // 2
                if nums[mid] < value: l = mid + 1
                else: r = mid
            return l
        first = lower_bound(target)
        if first == len(nums) or nums[first] != target:
            return [-1, -1]
        return [first, lower_bound(target + 1) - 1]
```

### LC 278
```python
# LeetCode provides isBadVersion(version).
class Solution:
    def firstBadVersion(self, n):
        left, right = 1, n
        while left < right:
            mid = (left + right) // 2
            if isBadVersion(mid): right = mid
            else: left = mid + 1
        return left
```

### LC 744
```python
class Solution:
    def nextGreatestLetter(self, letters, target):
        left, right = 0, len(letters)
        while left < right:
            mid = (left + right) // 2
            if letters[mid] <= target: left = mid + 1
            else: right = mid
        return letters[left % len(letters)]
```

### LC 1539
```python
class Solution:
    def findKthPositive(self, arr, k):
        left, right = 0, len(arr)
        while left < right:
            mid = (left + right) // 2
            missing = arr[mid] - (mid + 1)
            if missing < k: left = mid + 1
            else: right = mid
        return left + k
```
