# Level 1 — Classical Binary Search

**Status:** Completed. **Pattern:** exploit a monotonic sorted search space and discard half each iteration.

| LC | Problem | Key recognition | Complexity |
|---|---|---|---|
| 704 | Binary Search | Exact target in sorted array | O(log n) time, O(1) space |
| 35 | Search Insert Position | Lower bound: first position >= target | O(log n), O(1) |
| 69 | Sqrt(x) | Largest integer m where m² <= x | O(log x), O(1) |
| 367 | Valid Perfect Square | Search for integer m with m² == num | O(log num), O(1) |

## Invariant and common mistakes
For exact search, the target remains inside inclusive `[left,right]` if present. For lower bound, use a half-open interval `[left,right)`; the answer can be n. Avoid mixing `while left < right` with updates designed for `while left <= right`. For integer square root, return the best valid lower candidate, not simply the last midpoint.

## Python reference solutions (reconstructed, not imported submissions)

### LC 704
```python
class Solution:
    def search(self, nums, target):
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = left + (right - left) // 2
            if nums[mid] == target: return mid
            if nums[mid] < target: left = mid + 1
            else: right = mid - 1
        return -1
```

### LC 35
```python
class Solution:
    def searchInsert(self, nums, target):
        left, right = 0, len(nums)
        while left < right:
            mid = (left + right) // 2
            if nums[mid] < target: left = mid + 1
            else: right = mid
        return left
```

### LC 69
```python
class Solution:
    def mySqrt(self, x):
        left, right, best = 0, x, 0
        while left <= right:
            mid = (left + right) // 2
            if mid * mid <= x:
                best = mid
                left = mid + 1
            else:
                right = mid - 1
        return best
```

### LC 367
```python
class Solution:
    def isPerfectSquare(self, num):
        left, right = 1, num
        while left <= right:
            mid = (left + right) // 2
            sq = mid * mid
            if sq == num: return True
            if sq < num: left = mid + 1
            else: right = mid - 1
        return False
```
