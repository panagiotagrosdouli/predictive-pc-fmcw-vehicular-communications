# Paper-1 correction note

The September 2026 final reproducibility audit found a packet-deadline discretization defect in the historical Paper-1 simulator. A physical deadline converted to `N` slots was stored as `arrival + N` while the queue expiry test treated that value as an inclusive last-service slot. The result was an `N+1`-slot service window. In addition, the historical `deadline_0p05` regime requested 0.05 s while the simulator slot duration was 0.1 s, so that physical deadline was not exactly representable.

The corrected implementation uses `arrival + N - 1` as the inclusive last-service slot and fails closed when a physical deadline is not an integer number of simulator slots. The corrected tight-deadline regime is therefore 0.1 s. Historical run `34055071988`, `service_guarded_80`, and its 3/4 HELP statistics remain immutable pre-correction provenance and are not final corrected-model evidence.

The corrected protocol used fresh development seeds `20270101`--`20270110` and fresh holdout seeds `20270201`--`20270220`. It executed successfully in workflow run `34785876008` at SHA `2e3f48a3fa7597371d1fcb8ef505f40e2c52a1a1`. Artifact `10326910705` (`prospective-current-service-guard`) has digest `sha256:10ad8a88f4d8fa25216603b5e06171a464ab706adb9421793a3742b177127407`.

Corrected development selected `service_guarded_100` (guard ratio 1.0). On the fresh 20-seed holdout, all four predeclared primary goodput comparisons against Reactive Greedy are `NEUTRAL_OR_UNCERTAIN` under the frozen +/-0.001 Mbps practical-margin/95% CI rule. Final Paper-1 headline claims must use this corrected evidence only.
