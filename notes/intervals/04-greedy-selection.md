# Pattern 4 — Greedy interval selection

**Completed:** LC 435, LC 452, LC 646.

## Recognition
Choose a maximum compatible collection or minimum removals/resources. The crucial decision is which interval endpoint to preserve for the future.

## LC 435 — Non-overlapping Intervals
**From our discussion:** sorting by start also works. If `start >= prev_end`, keep the interval. Otherwise count one removal and keep the interval that **ends earlier** via `prev_end = min(prev_end, end)`.

```python
def eraseOverlapIntervals(intervals):
    intervals.sort(key=lambda x: x[0])
    removed = 0
    prev_end = float("-inf")
    for start, end in intervals:
        if start < prev_end:
            removed += 1
            prev_end = min(prev_end, end)
        else:
            prev_end = end
    return removed
```
Time O(n log n), extra scan space O(1), excluding sort.

**Key contrast from our study:** **LC 56 merges with `max(end)`** because it wants union; **LC 435 keeps `min(end)`** because it wants more available room for later intervals.

## LC 452 — Minimum Number of Arrows to Burst Balloons
**Pattern extension:** sort by ending coordinate. Place an arrow at the current earliest end; add another only when the next balloon starts strictly after that coordinate.

```python
def findMinArrowShots(points):
    if not points:
        return 0
    points.sort(key=lambda p: p[1])
    arrows, end = 1, points[0][1]
    for start, finish in points[1:]:
        if start > end:
            arrows += 1
            end = finish
    return arrows
```
Time O(n log n), extra scan space O(1).

## LC 646 — Maximum Length of Pair Chain
**Pattern extension:** selecting a maximum-length chain is an end-time greedy task. Here a pair (a,b) precedes (c,d) only if `b < c` (strict).

```python
def findLongestChain(pairs):
    pairs.sort(key=lambda p: p[1])
    count, last_end = 0, float("-inf")
    for start, end in pairs:
        if start > last_end:
            count += 1
            last_end = end
    return count
```
Time O(n log n), extra scan space O(1).

*LC 435 includes conversation-derived reasoning; remaining descriptions and all code are reconstructed, not imported submissions.*
