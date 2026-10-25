# Pattern 1 — Basic interval overlap

**Completed:** LC 252, LC 2446.

## Recognition
The question asks whether two time ranges clash, or whether any meeting conflicts with the next. First determine whether endpoints are inclusive or touching is allowed.

## LC 252 — Meeting Rooms
**From our discussion:** sort by starting time; if a meeting starts **before** the previous meeting ends, there is a conflict. Meetings where `start == previous_end` do not conflict.

```python
def canAttendMeetings(intervals):
    intervals.sort(key=lambda x: x[0])
    for i in range(1, len(intervals)):
        if intervals[i][0] < intervals[i - 1][1]:
            return False
    return True
```
Time O(n log n), extra scan space O(1), excluding sorting implementation.

## LC 2446 — Determine if Two Events Have Conflict
**From our discussion:** events have inclusive endpoints, so touching **does** count as conflict.

```python
def haveConflict(event1, event2):
    return event1[0] <= event2[1] and event2[0] <= event1[1]
```
Time O(1), space O(1). Fixed-width HH:MM timestamps compare lexicographically.

## Common mistake
Memorizing one comparison for every interval problem. **LC 252 uses strict `<`** at the boundary; **LC 2446 uses `<=`** because of inclusive semantics.

*Code samples are reconstructed study implementations, not imported personal submissions.*
