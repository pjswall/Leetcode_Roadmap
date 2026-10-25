# Pattern 3 — Insert and online booking

**Completed:** LC 57, LC 729.

## LC 57 — Insert Interval
**From our discussion:** input intervals are already sorted and non-overlapping. Think in **three regions**:
1. Intervals strictly before the new one: `end < new_start`.
2. Overlapping intervals: `start <= new_end`; expand the insertion range with `min(start)` and `max(end)`.
3. Remaining intervals, which come after the merged insertion.

```python
def insert(intervals, newInterval):
    ans, i, n = [], 0, len(intervals)
    start, end = newInterval
    while i < n and intervals[i][1] < start:
        ans.append(intervals[i]); i += 1
    while i < n and intervals[i][0] <= end:
        start = min(start, intervals[i][0])
        end = max(end, intervals[i][1])
        i += 1
    ans.append([start, end])
    ans.extend(intervals[i:])
    return ans
```
Time O(n), output O(n).

## LC 729 — My Calendar I
**Pattern extension (reconstructed, not a recovered chat explanation):** each booking is a half-open range `[start, end)`. Reject a new booking iff it overlaps an existing booking: `new_start < old_end and old_start < new_end`.

```python
class MyCalendar:
    def __init__(self):
        self.bookings = []

    def book(self, start, end):
        for s, e in self.bookings:
            if start < e and s < end:
                return False
        self.bookings.append((start, end))
        return True
```
Time O(n) per booking; O(n) stored intervals.

**Pitfall:** unlike inclusive event time ranges, `[10,20)` and `[20,30)` do not overlap.

*Code samples are reconstructed study implementations, not imported personal submissions.*
