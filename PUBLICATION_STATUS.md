# Publication Status — Paper 1 / Paper 2

## Overall status

This repository contains two deliberately separated scientific scopes. Publication status is scope-specific; green CI alone is not scientific evidence.

### Paper 1 — mechanism and operating-region study

**STATUS: CORRECTED-MODEL REVALIDATION REQUIRED BEFORE FINAL NUMERICAL CLAIMS.**

Paper 1 asks when causal future geometry/link information improves packet scheduling for the modeled PC-FMCW/DPSK vehicular optical link. The implementation, causal architecture, Part-A link provenance, synthetic development/holdout machinery, and paired analysis are present. During the September 2026 final audit, however, a packet-deadline discretization defect was found: an `N`-slot physical deadline was encoded with inclusive last-service index `arrival + N`, allowing `N+1` service slots. The historical 0.05 s regime was also not exactly representable with the 0.1 s simulator slot duration.

The simulator now uses `arrival + N - 1` and rejects physical deadlines that are not an integer number of slots. The corrected frozen protocol uses a 0.1 s tight-deadline regime plus the existing 0.5 s, load 1.1, and +3 dB SNR regimes, with fresh development seeds 20270101–20270110 and fresh holdout seeds 20270201–20270220. The guard family must be re-selected on corrected development data and evaluated once on the corrected holdout before Paper-1 headline statistics are restored.

The earlier run 34055071988 remains immutable historical provenance. Its raw 80 holdout rows were independently re-analyzed during the audit and reproduce the versioned means, bootstrap confidence intervals, Wilcoxon p-values, Holm adjustments, and paired Cohen dz values. Those statistics are therefore internally reproducible but **pre-correction** and must not be presented as final corrected-model evidence.

Paper 1 remains a model-based synthetic study. It does not claim measured end-to-end optical-channel validation, road deployment, hardware-in-the-loop validation, or globally optimal scheduling. The Part-A source is a supplied PC-FMCW/DPSK reference with a separately verified receiver-derived BER LUT; the local geometry/link path is reference-SNR anchored and its absolute received power is not calibrated to measured watts.

### Paper 2 — communication-aware learned trajectory prediction

**STATUS: INCOMPLETE / NOT PAPER READY.**

Paper 2 requires the canonical WOMD corpus/provenance, a complete 4-objective × 5-independent-seed learned archive, untouched held-out/OOD evaluation, learned predictor-to-link-to-packet evaluation, communication-aware objective ablations, paired multi-seed statistics, final figures/tables, and its own immutable manifest. Those gates are not satisfied by Paper-1 evidence and are not bypassed by green CI.

## Current software verification

At audit base `main` SHA `9e57ced0036300c90fddb9a4b5f155142a7f8e50`, CI run 34716692874 passed lint, 233 tests plus 20 subtests, stage-entrypoint checks, scientific monotonicity/causality validation, and Paper-1 LaTeX compilation. The combined Stage 0–8 entrypoint report still showed the learned/WOMD stages blocked by missing external inputs/artifacts; this is expected for Paper 2 and must not be conflated with Paper-1 readiness.

## Claim boundary

- Deployable schedulers may use only causal observations and forecasts; future ground truth is evaluator/realization information only.
- The independent inferential unit is the paired scenario/episode seed within regime, not packets or time samples.
- Synthetic/model-derived channel quantities are not measurements.
- Negative, null, and mixed outcomes remain part of the scientific record.
- No categorical first-of-kind claim is made for trajectory prediction, predictive scheduling, deadline-aware vehicular resource allocation, PC-FMCW, phase coding, or vehicular optical communication.
- The corrected Paper-1 manuscript must follow the corrected workflow artifact even if its results are weaker than the historical evidence.

## Readiness summary

**University Part B / Paper 1:** pending corrected-model revalidation and manuscript synchronization.

**Paper 1 external submission:** pending corrected evidence, final literature/claim synchronization, current CI/LaTeX/PDF audit, real author metadata, and a final provenance manifest. Even after those gates, the evidence remains synthetic/model-based rather than externally measured.

**Paper 2:** NOT PAPER READY.
