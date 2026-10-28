# Level 3 — Rotated Sorted Arrays

**Status:** Completed.

| LC | Problem | Progress | Recognition |
|---|---|---|---|
| 33 | Search in Rotated Sorted Array | Completed | Detect sorted half and discard impossible side |
| 81 | Search in Rotated Sorted Array II | Completed | Duplicates can hide sorted half |
| 153 | Find Minimum in Rotated Sorted Array | Completed | Compare midpoint to right boundary |
| 154 | Find Minimum in Rotated Sorted Array II | Completed | Equality can force linear shrinking |

## Core intuition

A rotated sorted array isn't globally sorted, but in the distinct case at least one side around the midpoint has useful ordering.

- **LC 33:** detect which half is sorted; check whether the target is in that value range.
- **LC 81:** when `nums[left] == nums[mid] == nums[right]`, equal values hide the sorted side; remove redundant boundaries.
- **LC 153:** `nums[mid] > nums[right]` puts the minimum strictly to the right; otherwise keep `mid` via `right = mid`.
- **LC 154:** when `nums[mid] == nums[right]`, safely discard a copy at `right` (but worst-case time becomes linear).

## Reference Python solutions

These examples are reconstructed, not imported accepted submissions.

### LC 33 — Search in Rotated Sorted Array
```python
class Solution:
    def search(self, nums, target):
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return mid
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

### LC 81 — Search in Rotated Sorted Array II
```python
class Solution:
    def search(self, nums, target):
        left, right = 0, len(nums) - 1
        while left <= right:
            mid = (left + right) // 2
            if nums[mid] == target:
                return True
            if nums[left] == nums[mid] == nums[right]:
                left += 1
                right -= 1
            elif nums[left] <= nums[mid]:
                if nums[left] <= target < nums[mid]:
                    right = mid - 1
                else:
                    left = mid + 1
            else:
                if nums[mid] < target <= nums[right]:
                    left = mid + 1
                else:
                    right = mid - 1
        return False
```

### LC 153 — Find Minimum in Rotated Sorted Array
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

### LC 154 — Find Minimum in Rotated Sorted Array II
```python
class Solution:
    def findMin(self, nums):
        left, right = 0, len(nums) - 1
        while left < right:
            mid = (left + right) // 2
            if nums[mid] > nums[right]:
                left = mid + 1
            elif nums[mid] < nums[right]:
                right = mid
            else:
                right -= 1
        return nums[left]
```

## Complexity
| Problem | Time | Extra space |
|---|---|---|
| 33 | O(log n) | O(1) |
| 81 | O(log n) typical, O(n) worst case | O(1) |
| 153 | O(log n) | O(1) |
| 154 | O(log n) typical, O(n) worst case | O(1) |

## Common mistakes
1. Incorrect inclusive / exclusive target boundaries for LC 33.
2. Missing LC 81's ambiguous duplicate branch.
3. Using `right = mid - 1` in LC 153, accidentally discarding the minimum.
4. Treating LC 154 equality as an ordered-half guarantee.

## Revision
Explain why LC 81 and 154 can degrade to O(n) and why LC 153 retains mid.
