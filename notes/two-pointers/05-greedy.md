# Level 5 — Greedy two pointers

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 11 — Container With Most Water](https://leetcode.com/problems/container-with-most-water/) | Move the shorter wall; keeping it cannot improve area with narrower width. | O(n) | O(1) |
| [LC 881 — Boats to Save People](https://leetcode.com/problems/boats-to-save-people/) | Sort: pair lightest with heaviest if possible; otherwise ship heaviest alone. | O(n log n) | O(1) scan + sorting |
| [LC 42 — Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) | Use left/right maxima; process the side with smaller known boundary. | O(n) | O(1) |
| [LC 1574 — Shortest Subarray to be Removed to Make Array Sorted](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/) | Find sorted prefix/suffix; then join them with two pointers. | O(n) | O(1) |

## What this level teaches

- Choosing which pointer to move
- Proving why discarding one side is safe
- Combining greedy reasoning with pointers

## Core technique

For each pointer move, give a proof that the discarded side cannot improve the optimal answer.

## Common mistakes and boundary cases

Always justify pointer movement via an invariant; for rainwater, update maxima in the proper order.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.


## Python reference implementations

### LC 11 — Container With Most Water
```python
class Solution:
    def maxArea(self, height):
        l, r, best = 0, len(height) - 1, 0
        while l < r:
            best = max(best, (r - l) * min(height[l], height[r]))
            if height[l] <= height[r]: l += 1
            else: r -= 1
        return best
```
### LC 881 — Boats to Save People
```python
class Solution:
    def numRescueBoats(self, people, limit):
        people.sort()
        l, r, boats = 0, len(people) - 1, 0
        while l <= r:
            if people[l] + people[r] <= limit: l += 1
            r -= 1
            boats += 1
        return boats
```
### LC 42 — Trapping Rain Water
```python
class Solution:
    def trap(self, height):
        l, r = 0, len(height) - 1
        left_max = right_max = water = 0
        while l <= r:
            if height[l] <= height[r]:
                left_max = max(left_max, height[l])
                water += left_max - height[l]
                l += 1
            else:
                right_max = max(right_max, height[r])
                water += right_max - height[r]
                r -= 1
        return water
```
### LC 1574 — Shortest Subarray to Be Removed
```python
class Solution:
    def findLengthOfShortestSubarray(self, arr):
        n = len(arr)
        left = 0
        while left + 1 < n and arr[left] <= arr[left + 1]: left += 1
        if left == n - 1: return 0
        right = n - 1
        while right > 0 and arr[right - 1] <= arr[right]: right -= 1
        best = min(n - left - 1, right)
        i, j = 0, right
        while i <= left and j < n:
            if arr[i] <= arr[j]:
                best = min(best, j - i - 1)
                i += 1
            else: j += 1
        return best
```
