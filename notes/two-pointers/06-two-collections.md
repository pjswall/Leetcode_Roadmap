# Level 6 — Two sorted collections and intervals

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 88 — Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/) | Merge from the back to avoid overwriting unread nums1 values. | O(m+n) | O(1) |
| [LC 986 — Interval List Intersections](https://leetcode.com/problems/interval-list-intersections/) | Take max starts and min ends; advance the interval ending first. | O(m+n) | O(1) excluding output |
| [LC 350 — Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/) | Sort both arrays; record an equal value, advancing both pointers. | O(m log m+n log n) | O(1) scan excluding output/sort |
| [LC 658 — Find K Closest Elements](https://leetcode.com/problems/find-k-closest-elements/) | After sorting, shrink a candidate range until exactly k elements remain. | O(n-k) for shrink on sorted input | O(1) extra excluding output |

## What this level teaches

- One pointer per collection
- Comparing current values
- Advancing only the relevant pointer
- Interval overlap logic

## Core technique

Use ordered inputs to avoid restarting scans. Compare current elements, take a useful action, then advance only pointers whose value or interval is no longer relevant.

## Common mistakes and boundary cases

LC 350's multiplicities matter; LC 986's overlap boundary is inclusive; LC 658 also admits binary search for left boundary.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.


## Python reference implementations

### LC 88 — Merge Sorted Array
```python
class Solution:
    def merge(self, nums1, m, nums2, n):
        i, j, k = m - 1, n - 1, m + n - 1
        while j >= 0:
            if i >= 0 and nums1[i] > nums2[j]:
                nums1[k] = nums1[i]
                i -= 1
            else:
                nums1[k] = nums2[j]
                j -= 1
            k -= 1
```
### LC 986 — Interval List Intersections
```python
class Solution:
    def intervalIntersection(self, firstList, secondList):
        i = j = 0
        ans = []
        while i < len(firstList) and j < len(secondList):
            start = max(firstList[i][0], secondList[j][0])
            end = min(firstList[i][1], secondList[j][1])
            if start <= end: ans.append([start, end])
            if firstList[i][1] < secondList[j][1]: i += 1
            else: j += 1
        return ans
```
### LC 350 — Intersection of Two Arrays II
```python
class Solution:
    def intersect(self, nums1, nums2):
        nums1.sort()
        nums2.sort()
        i = j = 0
        ans = []
        while i < len(nums1) and j < len(nums2):
            if nums1[i] == nums2[j]:
                ans.append(nums1[i])
                i += 1
                j += 1
            elif nums1[i] < nums2[j]: i += 1
            else: j += 1
        return ans
```
### LC 658 — Find K Closest Elements
```python
class Solution:
    def findClosestElements(self, arr, k, x):
        left, right = 0, len(arr) - 1
        while right - left + 1 > k:
            if x - arr[left] <= arr[right] - x: right -= 1
            else: left += 1
        return arr[left:right + 1]
```
