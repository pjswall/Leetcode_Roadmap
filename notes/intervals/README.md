# Intervals — Completed Track

**Status:** Fully Completed (user-confirmed) · **16 problems across 7 patterns**

| Pattern | Problems | Guide |
|---|---|---|
| Basic overlap | LC 252, 2446 | [01 — Overlap](01-overlap.md) |
| Merge / containment | LC 56, 1288 | [02 — Merge and containment](02-merge-containment.md) |
| Insert / online booking | LC 57, 729 | [03 — Insert and booking](03-insert-booking.md) |
| Greedy selection | LC 435, 452, 646 | [04 — Greedy](04-greedy-selection.md) |
| Resource allocation / min-heap | LC 253, 2406 | [05 — Heap allocation](05-resource-allocation.md) |
| Two-list intersections | LC 986, 1229 | [06 — Intersections](06-intersections.md) |
| Sweep line / difference events | LC 1094, 731, 732 | [07 — Sweep line](07-sweep-line.md) |

## Pattern recognition shortcuts

- **Any overlap?** Sort by start or compare interval endpoints.
- **Union of overlapping intervals?** Merge and extend to the **maximum end**.
- **Covered by another?** Sort start ascending, end descending.
- **Insert into sorted non-overlapping set?** Before / overlap / after phases.
- **Maximum compatible intervals?** End-time greedy; prioritize **minimum end**.
- **Minimum simultaneous resources?** Heap of end times or start/end sweep.
- **Two sorted interval lists?** Compute intersection and advance earlier-ending list.
- **Concurrent occupancy / bookings?** Difference events + running prefix count.

## Boundary warning

Whether equal endpoints conflict depends on problem semantics. For example, LC 252 and 729 allow a meeting to start exactly when another ends, while LC 2446 and 2406 consider inclusive endpoints overlapping.

## Provenance

These are curated study guides for the completed track, based on available learning context and standard algorithmic reconstructions. They are **not verbatim exports of the original project chat**. Python code snippets are illustrative reference implementations, **not claimed to be the learner's accepted submissions**.
