# Pattern 5 — Resource allocation with a min-heap

**Completed:** LC 253, LC 2406.

## Recognition
Find the **maximum number of simultaneously active intervals** or equivalently the minimum number of rooms/groups. A min-heap stores when the currently used resources become free.

## LC 253 — Meeting Rooms II
**Earlier discussion:** sort meeting times; use a min-heap of ending times or a start/end sweep-line pointer approach. Rooms can be reused when `earliest_end <= new_start` because touching meetings do not overlap.

```python
import heapq

def minMeetingRooms(intervals):
    heap = []
    for start, end in sorted(intervals):
        if heap and heap[0] <= start:
            heapq.heappop(heap)
        heapq.heappush(heap, end)
    return len(heap)
```
Time O(n log n), heap space O(n). This allocation version is valid for intervals processed in start order; reuse one room per new meeting.

## LC 2406 — Divide Intervals Into Minimum Number of Groups
**Pattern extension:** the ranges are **inclusive**, so intervals touching at a value conflict. Reuse a group only when `earliest_end < start` (strict).

```python
import heapq

def minGroups(intervals):
    heap = []
    for start, end in sorted(intervals):
        if heap and heap[0] < start:
            heapq.heappop(heap)
        heapq.heappush(heap, end)
    return len(heap)
```
Time O(n log n), heap space O(n).

## Common mistake
Reusing the same equality rule in both tasks. Meeting-room endpoints are compatible at equality, but inclusive LC 2406 groups are not.

*Notes combine recorded topic guidance with reconstructed implementations, not imported submissions.*
