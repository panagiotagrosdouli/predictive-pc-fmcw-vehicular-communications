# Publication Status — Paper 1 / Paper 2

## Overall status

This repository contains two deliberately separated scientific scopes. Publication status is scope-specific; green CI alone is not scientific evidence.

### Paper 1 — mechanism and operating-region study

**STATUS: CORRECTED PRIMARY EVIDENCE EXECUTED; FINAL MANUSCRIPT/CI GATES IN PROGRESS.**

During the September 2026 final audit, a packet-deadline discretization defect was found: an `N`-slot physical deadline had been encoded with inclusive last-service index `arrival + N`, allowing `N+1` service slots. The historical 0.05 s regime was also not exactly representable with the 0.1 s simulator slot duration. The simulator now uses `arrival + N - 1` and rejects non-integral physical deadlines.

A fresh corrected protocol was executed in workflow run `34785876008` at SHA `2e3f48a3fa7597371d1fcb8ef505f40e2c52a1a1`. Artifact `10326910705` (`prospective-current-service-guard`) has digest `sha256:10ad8a88f4d8fa25216603b5e06171a464ab706adb9421793a3742b177127407`. Development seeds `20270101`–`20270110` and holdout seeds `20270201`–`20270220` are disjoint from each other and from the historical service-guard evidence.

The corrected development selection chose `service_guarded_100` (guard ratio 1.0). On the fresh 20-seed holdout, all four predeclared primary goodput comparisons against Reactive Greedy are **NEUTRAL_OR_UNCERTAIN** under the frozen ±0.001 Mbps practical-margin/95% CI rule:

- deadline 0.1 s: +0.00000 Mbps, CI [0.00000, 0.00000];
- deadline 0.5 s: +0.00035 Mbps, CI [0.00000, 0.00105];
- offered load 1.1: -0.00050 Mbps, CI [-0.00455, 0.00285];
- reference SNR +3 dB: +0.00080 Mbps, CI [-0.00080, 0.00255].

All Holm-adjusted p-values are 1.0. The corrected evidence therefore does **not** support the historical headline that the guarded predictive scheduler improves three of four regimes. That historical run remains immutable pre-correction provenance only.

Paper 1 remains a model-based synthetic mechanism study. The corrected result is a defensible null/mixed finding: future information can alter candidate decisions in diagnostics, but the robust guard selected under the frozen cross-regime development rule largely removes incremental packet-level benefit on holdout. No measured end-to-end optical-channel validation, road deployment, hardware-in-the-loop validation, or globally optimal scheduling is claimed.

### Paper 2 — communication-aware learned trajectory prediction

**STATUS: INCOMPLETE / NOT PAPER READY.**

Paper 2 requires the canonical WOMD corpus/provenance, a complete 4-objective × 5-independent-seed learned archive, untouched held-out/OOD evaluation, learned predictor-to-link-to-packet evaluation, communication-aware objective ablations, paired multi-seed statistics, final figures/tables, and its own immutable manifest. Those gates are not satisfied by Paper-1 evidence and are not bypassed by green CI.

## Current software verification

The corrected evidence workflow passed static checks, unit tests, frozen development/holdout execution, cardinality verification, frozen holdout analysis, and artifact upload. A final general CI/LaTeX run is still required on the fully synchronized manuscript branch head because publication text changes after evidence generation must themselves be build-verified.

## Claim boundary

- Deployable schedulers may use only causal observations and forecasts; future ground truth is evaluator/realization information only.
- The independent inferential unit is the paired scenario/episode seed within regime, not packets or time samples.
- Synthetic/model-derived channel quantities are not measurements.
- Negative, null, and mixed outcomes remain part of the scientific record.
- No categorical first-of-kind claim is made for trajectory prediction, predictive scheduling, deadline-aware vehicular resource allocation, PC-FMCW, phase coding, or vehicular optical communication.
- Historical pre-correction statistics must not be presented as corrected-model evidence.

## Readiness summary

**University Part B / Paper 1:** corrected primary evidence executed; manuscript/provenance synchronization and final CI/PDF audit remain.

**Paper 1 external submission:** still requires final literature/claim consistency, current CI/LaTeX/PDF audit, real author metadata, and final provenance review. Even after those gates, the evidence remains synthetic/model-based rather than externally measured.

**Paper 2:** NOT PAPER READY.
