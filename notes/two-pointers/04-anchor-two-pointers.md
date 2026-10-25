# Level 4 — Anchor plus two pointers

**Track:** Two Pointers · **Overall topic status:** Fully Completed (user confirmed).

## Problem order and recognition

| Problem | Recognition and optimal intuition | Time | Extra space |
|---|---|---|---|
| [LC 15 — 3Sum](https://leetcode.com/problems/3sum/) | Sort, fix an anchor, search opposing ends; skip duplicate triplets. | O(n²) | O(1) extra, excluding output/sort |
| [LC 16 — 3Sum Closest](https://leetcode.com/problems/3sum-closest/) | Keep nearest encountered total while moving pointers by sum comparison. | O(n²) | O(1) extra |
| [LC 18 — 4Sum](https://leetcode.com/problems/4sum/) | Fix two anchors, two-pointer scan the remaining sorted range. | O(n³) | O(1) extra, excluding output/sort |
| [LC 259 — 3Sum Smaller](https://leetcode.com/problems/3sum-smaller/) | When sum is below target, bulk-count right-left valid pairs for anchor. | O(n²) | O(1) extra |

## What this level teaches

- Sorting first
- Fixing one element
- Searching the remaining range
- Duplicate handling

## Core technique

Sorting converts search for a pair under a fixed anchor to a linear opposing-pointer sweep. Separate uniqueness constraints from counting constraints.

## Common mistakes and boundary cases

In counting problems, bulk-count valid ranges; in unique tuple output problems, skip duplicate anchors and duplicates after a match.

## Revision checklist

- Explain the recognition clue without using the level name.
- State the invariant and why pointer movement is safe.
- Write the Python solution independently and test minimum-size and boundary inputs.
- Compare against brute force and state time/space complexity.

> These are curated reference notes from the supplied level/problem outline with added standard algorithm intuition and complexities. They are not verbatim exports of past chats, and no personal code submissions are claimed.


## Python reference implementations

### LC 15 — 3Sum
```python
class Solution:
    def threeSum(self, nums):
        nums.sort()
        ans = []
        for i in range(len(nums) - 2):
            if i and nums[i] == nums[i - 1]: continue
            l, r = i + 1, len(nums) - 1
            while l < r:
                total = nums[i] + nums[l] + nums[r]
                if total < 0: l += 1
                elif total > 0: r -= 1
                else:
                    ans.append([nums[i], nums[l], nums[r]])
                    l += 1
                    r -= 1
                    while l < r and nums[l] == nums[l - 1]: l += 1
                    while l < r and nums[r] == nums[r + 1]: r -= 1
        return ans
```
### LC 16 — 3Sum Closest
```python
class Solution:
    def threeSumClosest(self, nums, target):
        nums.sort()
        best = sum(nums[:3])
        for i in range(len(nums) - 2):
            l, r = i + 1, len(nums) - 1
            while l < r:
                total = nums[i] + nums[l] + nums[r]
                if abs(total - target) < abs(best - target): best = total
                if total < target: l += 1
                elif total > target: r -= 1
                else: return target
        return best
```
### LC 18 — 4Sum
```python
class Solution:
    def fourSum(self, nums, target):
        nums.sort()
        ans, n = [], len(nums)
        for i in range(n - 3):
            if i and nums[i] == nums[i - 1]: continue
            for j in range(i + 1, n - 2):
                if j > i + 1 and nums[j] == nums[j - 1]: continue
                l, r = j + 1, n - 1
                while l < r:
                    total = nums[i] + nums[j] + nums[l] + nums[r]
                    if total < target: l += 1
                    elif total > target: r -= 1
                    else:
                        ans.append([nums[i], nums[j], nums[l], nums[r]])
                        l += 1
                        r -= 1
                        while l < r and nums[l] == nums[l - 1]: l += 1
                        while l < r and nums[r] == nums[r + 1]: r -= 1
        return ans
```
### LC 259 — 3Sum Smaller
```python
class Solution:
    def threeSumSmaller(self, nums, target):
        nums.sort()
        count = 0
        for i in range(len(nums) - 2):
            l, r = i + 1, len(nums) - 1
            while l < r:
                if nums[i] + nums[l] + nums[r] < target:
                    count += r - l
                    l += 1
                else:
                    r -= 1
        return count
```
