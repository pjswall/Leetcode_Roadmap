# Level 3 — Rotated Sorted Arrays

**Status:** In progress. **LC 33** is supplied in the current level outline; **LC 153** is the previously confirmed *current problem* (level 3, problem 2).

| LC | Problem | Progress | Recognition |
|---|---|---|---|
| 33 | Search in Rotated Sorted Array | First problem in supplied sequence; per-problem submission unverified | One side of the midpoint is sorted |
| 153 | Find Minimum in Rotated Sorted Array | **Current — Learning** | Compare midpoint against right boundary to locate pivot |

## Key insight
A rotated array is not globally sorted, but **one half** remains sorted. For LC 33, determine which half is ordered, then test whether the target lies in that half. For LC 153 (distinct values), `nums[mid] > nums[right]` means the minimum lies **after mid**; otherwise it lies in `[left,mid]`. Keeping mid in the second case avoids discarding the answer.

## Python reference solutions (reconstructed; LC 153 not claimed as solved)

### LC 33
```python
class Solution:
    def search(self, nums, target):
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target: return mid
            if nums[left] <= nums[mid]:
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1
        return -1
```

### LC 153
```python
class Solution:
    def findMin(self, nums):
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[right]:
                left = mid + 1
            else:
                right = mid
        return nums[left]
```

**Complexity:** Both O(log n) time, O(1) extra space under their distinct-element constraints.

**Common mistake:** For LC 153, `right = mid - 1` in the second branch can skip the minimum. With duplicates, recognition is trickier (LC 81/154 are separate variants).

## Revision prompt
Can you explain the invariants for LC 33 and LC 153 without recalling code? Which comparison drives each branch?
