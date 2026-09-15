# Paper 1 Mechanism Diagnostic Protocol

Status: **FROZEN BEFORE CORRECTED MECHANISM EXECUTION**

Evidence tier: **DIAGNOSTIC / MECHANISTIC / SECONDARY**. This protocol does not replace, modify, reinterpret, or tune the frozen corrected primary holdout. The primary confirmatory evidence remains the corrected `service_guarded_100` holdout on seeds 20270201--20270220 with the pre-specified practical margin and multiplicity procedure.

## Purpose

Test the mechanism-level question: when does future mobility information become actionable at packet level, and when is it redundant with current link/queue state? The diagnostic is explanatory rather than a new confirmatory endpoint.

## Frozen diagnostic questions

1. How often do causal predictive/link-lifetime policies make a different service decision from Reactive Greedy?
2. When policies disagree, what realized link/queue state is selected and what packet-level metrics result?
3. How much additional packet-level utility is available to a non-deployable future-ground-truth oracle under the same synthetic regimes?
4. Do the answers vary across deadline, offered-load, and SNR regimes?

## Policies

The existing diagnostic implementation evaluates `reactive_greedy`, `predictive_utility`, `link_lifetime`, `deadline_aware_lifetime`, and `oracle`. The oracle is evaluator-only and non-deployable; future ground truth must not enter a deployable scheduler.

The frozen primary policy `service_guarded_100` is not replaced by this diagnostic scheduler family. Any relationship between these diagnostic policies and the primary selected policy must be described explicitly rather than implied.

## Regimes

The corrected diagnostic regimes are frozen as:

- `deadline_0p1`: physical deadline 0.1 s;
- `deadline_0p5`: physical deadline 0.5 s;
- `load_1p1`: offered load 1.1;
- `snr_plus3`: reference SNR offset +3 dB.

With the repository time step `dt = 0.1 s`, the historical 0.05 s deadline is nonrepresentable and is excluded from corrected mechanism evidence. Deadline semantics use the last legal service slot `arrival + N - 1` for an N-slot deadline.

## Seeds and independence

Diagnostic seeds are frozen as 20260827, 20260828, 20260829, 20260830, and 20260831. They predate this strengthening pass and are retained without post-result selection. They are disjoint from the corrected development seeds 20270101--20270110 and frozen primary holdout seeds 20270201--20270220.

The inferential/descriptive unit is the paired scenario/episode seed within a regime. Slots and packets are not to be treated as independent experimental replicates.

## Decision metrics

For the pre-existing policy pairs, record per paired seed:

- all-slot agreement;
- fraction where both schedulers are active;
- agreement conditional on both being active;
- both-active disagreement fraction;
- A-only active fraction;
- B-only active fraction.

For each scheduler also record selected-state and packet-level summaries already exposed by the simulator:

- realized outage of the selected vehicle;
- realized SNR of the selected vehicle;
- mean queue occupancy at selection;
- goodput;
- packet-delivery ratio;
- p95 latency;
- demand-normalized Jain fairness.

Beneficial/harmful/neutral disagreement, deadline-urgency alignment, and service-guard suppression may be reported only if additional instrumentation exposes them unambiguously. They must not be inferred from aggregate metrics alone.

## Oracle definition and interpretation

`oracle` is a non-deployable evaluator that may use future ground truth only to estimate an upper-bound/value-of-information reference under the simulator's own assumptions. It is not a causal scheduler and is not a candidate for deployment.

Interpret the diagnostic without forcing a desired ordering. In particular, distinguish: (A) oracle approximately reactive and causal approximately reactive; (B) oracle better than reactive while causal approximately reactive; (C) oracle better than causal better than reactive; and (D) regime-dependent/mixed ordering. Report the observed pattern even if it weakens the proposed mechanism story.

## Operating-region and forecast-quality extensions

No additional operating-region grid, guard-strength sweep, or forecast-noise perturbation is frozen in this protocol. Such experiments must not be improvised after seeing these results. If a scientifically justified extension is needed, freeze a separate addendum with exact grid/seeds/metrics before executing it.

## Analysis discipline

The decision audit is descriptive/mechanistic. Report paired-seed distributions, means/medians and uncertainty where supportable. Do not convert slot-level observations into pseudo-replicates. Any new family of formal hypothesis tests requires an explicit multiplicity plan before testing.

The frozen corrected primary statistical analysis remains unchanged. Diagnostic results may explain or bound the primary null/mixed finding but may not replace it or be represented as confirmatory evidence.

## Reproducibility

Canonical corrected execution is through `scripts/08_run_decision_audit.py` and the `Decision-level mechanism audit` GitHub Actions workflow. Saved diagnostic artifacts must identify the evidence tier, seeds, policies and corrected regimes. Publication figures or prose using these outputs must trace to the saved artifact and source SHA.
