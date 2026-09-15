# Paper 1 Final Scientific Protocol

**Scope:** PAPER1

## Research question

When, why, and under which operating regimes does causal trajectory/link prediction change packet-level scheduling for the model-based PC-FMCW/DPSK vehicular optical link relative to reactive scheduling, and when does that information fail to provide robust packet-level value?

## Contribution

Paper 1 is a causal cross-layer mechanism study. Observed vehicle history is mapped to future relative geometry; the PC-FMCW/DPSK-informed link model maps that geometry to future link utility; queues, deadlines, current service opportunity, and predicted link lifetime determine scheduling decisions. The confirmatory method includes a prospectively selected current-service guard that limits future-urgency actions when they sacrifice immediate service opportunity.

## Causality and fairness

Deployable methods may use observations available at or before the decision slot only. Future ground truth is reserved for realization/evaluation and the explicitly labeled Oracle information reference. All paired scheduler comparisons share scenario, traffic realization, packet deadlines, and transmission random numbers. The independent experimental unit is the paired scenario/episode seed within regime, never an individual packet or time sample.

## Deadline correction and evidence reset

The September 2026 audit found that the historical simulator encoded an N-slot physical deadline with inclusive last-service index `arrival + N`, allowing N+1 service opportunities. The corrected implementation uses `arrival + N - 1`. Physical deadlines must be exactly representable as an integer number of simulator slots; the historical 0.05 s regime is therefore invalid at the 0.1 s slot duration and remains pre-correction provenance only.

Historical workflow run `34055071988`, the historical `service_guarded_80` selection, and its 3/4 HELP result are not corrected-model evidence.

## Corrected primary confirmatory comparison

The corrected prospective protocol used development seeds `20270101`--`20270110` and disjoint holdout seeds `20270201`--`20270220`. The frozen development rule selected `service_guarded_100` (guard ratio 1.0) before holdout inspection.

The four corrected predeclared regimes are:

- deadline = 0.1 s;
- deadline = 0.5 s;
- offered load = 1.1;
- reference-SNR offset = +3 dB.

Primary endpoint: paired candidate-minus-Reactive-Greedy goodput difference within each regime, with 20 paired holdout seeds per regime.

Inference: 100,000 paired percentile bootstrap replicates, 95% CI for the mean paired difference, two-sided paired Wilcoxon signed-rank test, Holm correction across the four primary comparisons, paired Cohen dz, and win/loss/tie fractions. Practical margin is +/-0.001 Mbps. HELP requires the lower CI bound > +0.001 Mbps; HURT requires the upper CI bound < -0.001 Mbps; otherwise the result is NEUTRAL_OR_UNCERTAIN. For an all-zero contrast, the Wilcoxon test is degenerate and the multiplicity-adjusted value is conservatively recorded as 1.0.

The corrected execution is workflow run `34785876008` at SHA `2e3f48a3fa7597371d1fcb8ef505f40e2c52a1a1`, artifact `10326910705` (`prospective-current-service-guard`), digest `sha256:10ad8a88f4d8fa25216603b5e06171a464ab706adb9421793a3742b177127407`.

## Corrected primary result

All four corrected holdout comparisons are NEUTRAL_OR_UNCERTAIN under the frozen practical-margin/95% CI rule:

| Regime | Mean delta goodput (Mbps) | 95% CI | Holm p | Cohen dz |
|---|---:|---:|---:|---:|
| deadline 0.1 s | +0.00000 | [0.00000, 0.00000] | 1.0 | 0.000 |
| deadline 0.5 s | +0.00035 | [0.00000, 0.00105] | 1.0 | 0.224 |
| load 1.1 | -0.00050 | [-0.00455, 0.00285] | 1.0 | -0.060 |
| SNR +3 dB | +0.00080 | [-0.00080, 0.00255] | 1.0 | 0.208 |

This result does not support the historical headline that guarded predictive scheduling improves three of four regimes. It supports a narrower mechanism conclusion: future information can alter candidate decisions, but the robust guard selected by the frozen cross-regime development rule largely removes incremental packet-level benefit on the fresh corrected holdout.

## Secondary outcomes and diagnostics

PDR, deadline/censoring outcomes, latency, fairness, queue behavior, scheduled-link quality, outage, link lifetime, operating-region sweeps, and historical service-order diagnostics are secondary or diagnostic unless separately preregistered. They may explain mechanisms and trade-offs but must not be promoted into undeclared corrected primary hypotheses.

## Claim boundary

The optical link is a PC-FMCW/DPSK-informed analytical/simulation model. Part-A physical-layer parameters and receiver evidence provide model provenance but do not constitute measured end-to-end vehicular optical calibration. No simulated optical-channel quantity is a physical measurement. No road deployment, hardware-in-the-loop validation, or measured vehicular optical-channel validation is claimed. Oracle is an evaluator-only information reference, not a globally optimal offline scheduler.

## Paper-1 / Paper-2 boundary

Paper 1 does not depend on incomplete GRU/WOMD learned-model claims. Learned communication-aware training and its 20-checkpoint study belong to Paper 2. Paper 1 may mention learned prediction only as future/parallel work, not as evidence for its primary claim.

## Canonical evidence rule

Corrected Paper-1 numerical claims must trace to `artifacts/paper1_final/primary_statistics.json` and the corrected workflow/artifact provenance above. Historical pre-correction outputs may be retained only with an explicit historical/pre-correction label. Missing external-data experiments must be reported as missing rather than imputed or invented.
