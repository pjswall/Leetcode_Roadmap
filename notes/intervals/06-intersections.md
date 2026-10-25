# Pattern 6 — Two sorted interval lists

**Completed:** LC 986, LC 1229.

## Recognition
Two lists are individually sorted by start time. Keep one pointer for each list, process only their current pair, and advance whichever interval **ends first**.

## LC 986 — Interval List Intersections
Intersection of `[a0,a1]` and `[b0,b1]` is `[max(a0,b0), min(a1,b1)]` if the new start is <= the new end. Touching inclusive ranges intersect at one point.

```python
def intervalIntersection(firstList, secondList):
    i = j = 0
    ans = []
    while i < len(firstList) and j < len(secondList):
        start = max(firstList[i][0], secondList[j][0])
        end = min(firstList[i][1], secondList[j][1])
        if start <= end:
            ans.append([start, end])
        if firstList[i][1] < secondList[j][1]:
            i += 1
        else:
            j += 1
    return ans
```
Time O(m+n), output O(min(m+n, number of intersections) to O(m+n) overall).

## LC 1229 — Meeting Scheduler
**Pattern extension:** same intersection calculation but test whether overlap length is at least `duration`. Return the earliest start.

```python
def minAvailableDuration(slots1, slots2, duration):
    slots1.sort()
    slots2.sort()
    i = j = 0
    while i < len(slots1) and j < len(slots2):
        start = max(slots1[i][0], slots2[j][0])
        end = min(slots1[i][1], slots2[j][1])
        if end - start >= duration:
            return [start, start + duration]
        if slots1[i][1] < slots2[j][1]:
            i += 1
        else:
            j += 1
    return []
```
Time O(m log m + n log n) if unsorted; pointer pass O(m+n). Extra sort space depends on implementation.

**Reasoning:** advancing the earlier-ending interval cannot miss a later overlap, since it has already ended.

*Concepts are aligned with the track; detailed code is reconstructed rather than extracted verbatim.*
