# Paper-1 correction note

The September 2026 final reproducibility audit found a packet-deadline discretization defect in the historical Paper-1 simulator. A physical deadline converted to `N` slots was stored as `arrival + N` while the queue expiry test treated that value as an inclusive last-service slot. The result was an `N+1`-slot service window. In addition, the historical `deadline_0p05` regime requested 0.05 s while the simulator slot duration was 0.1 s, so that physical deadline was not exactly representable.

The corrected implementation now uses `arrival + N - 1` as the inclusive last-service slot and fails closed when a physical deadline is not an integer number of simulator slots. The corrected tight-deadline regime is therefore 0.1 s. Historical run 34055071988 and its statistics remain immutable provenance and are not final corrected-model evidence.

The corrected protocol uses fresh development seeds 20270101–20270110 and fresh holdout seeds 20270201–20270220. Final manuscript headline numbers must be populated only from the resulting corrected workflow artifact. Until that artifact passes, the manuscript is scientifically pending corrected-model revalidation.
