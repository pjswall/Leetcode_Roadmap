# Pattern 2 — Merge and containment

**Completed:** LC 56, LC 1288.

## LC 56 — Merge Intervals
**Recognition:** ranges can overlap and the task is to return their union.

**From our discussion:** sort by start. Compare with the last interval already in `merged`: overlap when `start <= merged[-1][1]`, then extend the existing interval by taking `max(previous_end, current_end)`. Using `max` matters for **nested intervals** — never shrink the union.

```python
def merge(intervals):
    intervals.sort(key=lambda x: x[0])
    merged = []
    for start, end in intervals:
        if not merged or start > merged[-1][1]:
            merged.append([start, end])
        else:
            merged[-1][1] = max(merged[-1][1], end)
    return merged
```
Time O(n log n). Output O(n), with sorting-space implementation details.

**Mistake we explicitly discussed:** changing a scalar variable named `previous` does not automatically mutate `merged[-1]`. Append only when the new interval is non-overlapping.

## LC 1288 — Remove Covered Intervals
**Recognition:** remove intervals entirely contained within another, not just overlapping.

**From our discussion:** A covers B when `A.start <= B.start` and `A.end >= B.end`. Sort by start ascending and end descending, then maintain the maximum end seen so far.

```python
def removeCoveredIntervals(intervals):
    intervals.sort(key=lambda x: (x[0], -x[1]))
    max_end = float("-inf")
    remaining = 0
    for _, end in intervals:
        if end > max_end:
            remaining += 1
            max_end = end
    return remaining
```
Time O(n log n), extra scan space O(1), excluding sorting.

**Pitfall:** for identical starts, sort longer ranges first; otherwise a shorter interval might be counted before its covering interval.

*Code samples are reconstructed study implementations, not imported personal submissions.*
