# Pattern 7 — Sweep line and difference events

**Completed:** LC 1094, LC 731, LC 732.

## Recognition
You need the number of **currently active** intervals at points in time, possibly after online bookings. Transform ranges to start/end events and accumulate the running total in sorted time order.

## LC 1094 — Car Pooling
A trip `[passengers, start, end]` adds passengers at `start` and removes them at `end` (dropoff can occur before pickup at the same location).

```python
from collections import defaultdict

def carPooling(trips, capacity):
    events = defaultdict(int)
    for people, start, end in trips:
        events[start] += people
        events[end] -= people
    onboard = 0
    for location in sorted(events):
        onboard += events[location]
        if onboard > capacity:
            return False
    return True
```
Time O(n log n), event space O(n).

## LC 731 — My Calendar II
Allow double booking, **reject triple booking**. Maintain a delta map, tentatively increment at start and decrement at end, scan cumulative count; roll back if maximum exceeds 2.

```python
from collections import defaultdict

class MyCalendarTwo:
    def __init__(self):
        self.delta = defaultdict(int)

    def book(self, start, end):
        self.delta[start] += 1
        self.delta[end] -= 1
        active = 0
        for t in sorted(self.delta):
            active += self.delta[t]
            if active > 2:
                self.delta[start] -= 1
                self.delta[end] += 1
                return False
        return True
```
Time O(k log k) per booking with k event keys; O(k) space.

## LC 732 — My Calendar III
Return the maximum concurrent bookings after every insertion.

```python
from collections import defaultdict

class MyCalendarThree:
    def __init__(self):
        self.delta = defaultdict(int)

    def book(self, start, end):
        self.delta[start] += 1
        self.delta[end] -= 1
        active = best = 0
        for t in sorted(self.delta):
            active += self.delta[t]
            best = max(best, active)
        return best
```
Time O(k log k) per booking; O(k) space. For larger constraints, balanced search trees/segment trees can improve repeated scans.

## Common mistake
If event times tie, ordering matters. Aggregating start/end deltas at each time avoids accidental simultaneous counts for half-open intervals `[start,end)`.

*These are reconstructed explanations and reference implementations; personal submissions were not available.*
