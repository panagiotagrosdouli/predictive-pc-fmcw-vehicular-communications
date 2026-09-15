# Paper 1 Completion Audit — Corrected Evidence

**Scope:** PAPER1 — mechanism / operating-region study  
**Repository:** `panagiotagrosdouli/predictive-pc-fmcw-vehicular-communications`  
**Evidence boundary:** model-based PC-FMCW/DPSK-informed simulation; no measured optical-link or real-world vehicular validation claim.

## 1. Audit correction

The September 2026 final reproducibility audit found a packet-deadline discretization defect in the historical Paper-1 simulator. An N-slot physical deadline had been represented by inclusive last-service index `arrival + N`, allowing N+1 service slots. The historical 0.05 s deadline was also not exactly representable with the 0.1 s simulator slot duration.

The corrected implementation uses `arrival + N - 1` and rejects non-integral physical deadlines. Consequently, historical workflow run `34055071988`, the historical `service_guarded_80` selection, and the historical 3/4 HELP result are pre-correction provenance only and are not final Paper-1 evidence.

## 2. Corrected executed evidence

The corrected prospective protocol was executed in workflow run `34785876008` at source SHA `2e3f48a3fa7597371d1fcb8ef505f40e2c52a1a1`. The uploaded artifact is ID `10326910705`, name `prospective-current-service-guard`, digest `sha256:10ad8a88f4d8fa25216603b5e06171a464ab706adb9421793a3742b177127407`.

Development seeds `20270101`--`20270110` and holdout seeds `20270201`--`20270220` are disjoint. The corrected development rule selected `service_guarded_100` (guard ratio 1.0) before holdout inspection.

The four corrected predeclared regimes are deadline 0.1 s, deadline 0.5 s, offered load 1.1, and reference SNR +3 dB.

## 3. Corrected primary statistics

The primary endpoint is paired candidate-minus-Reactive-Greedy goodput. The independent inferential unit is the paired episode/seed within regime. The frozen analysis uses 100,000 paired percentile bootstrap replicates, 95% confidence intervals, two-sided paired Wilcoxon signed-rank tests, Holm correction across four comparisons, paired Cohen dz, and a +/-0.001 Mbps practical margin.

| Regime | Mean delta goodput (Mbps) | 95% CI | Holm p | Cohen dz | Classification |
|---|---:|---:|---:|---:|---|
| deadline 0.1 s | +0.00000 | [0.00000, 0.00000] | 1.0 | 0.000 | NEUTRAL_OR_UNCERTAIN |
| deadline 0.5 s | +0.00035 | [0.00000, 0.00105] | 1.0 | 0.224 | NEUTRAL_OR_UNCERTAIN |
| load 1.1 | -0.00050 | [-0.00455, 0.00285] | 1.0 | -0.060 | NEUTRAL_OR_UNCERTAIN |
| SNR +3 dB | +0.00080 | [-0.00080, 0.00255] | 1.0 | 0.208 | NEUTRAL_OR_UNCERTAIN |

For deadline 0.1 s all paired differences are zero; the Wilcoxon test is therefore degenerate and the corrected summary conservatively records Holm-adjusted p = 1.0. The other corrected raw Wilcoxon p-values are 0.3173, 1.0, and 0.2733; all Holm-adjusted p-values are 1.0.

## 4. Scientific interpretation

The corrected evidence does not support a claim that the guarded predictive scheduler improves three of four regimes. It also does not prove that predictive and reactive policies are universally identical.

The defensible result is a null/mixed mechanism finding: future information can alter candidate decisions in diagnostics, but the robust current-service guard selected by the frozen cross-regime development rule largely removes incremental packet-level benefit on the fresh holdout. Protecting immediate service opportunity suppresses harmful reordering, but at guard ratio 1.0 it also leaves little opportunity for predictive reordering to improve realized goodput.

## 5. Claim boundary and novelty

Paper 1 must not make categorical first-of-kind claims for trajectory prediction in VLC, predictive vehicular scheduling, deadline-aware resource allocation, PC-FMCW, phase coding, or vehicular optical communication. Prior work exists on trajectory prediction for dynamic VLC and on resource utilization/lifetime in VLC-based vehicular networks.

The contribution is narrower: a causal, auditable trajectory-to-link-to-packet mechanism study with explicit queue/deadline scheduling, ground-truth-derived realization, prospective guard selection, paired holdout inference, and preservation of null/negative findings.

The optical channel remains analytical/model-based. No measured end-to-end optical-channel validation, road deployment, hardware-in-the-loop validation, or globally optimal scheduling is claimed.

## 6. Paper-1 / Paper-2 separation

Paper 1 is the classical/mechanism study and does not depend on incomplete learned GRU/WOMD evidence. Paper 2 remains incomplete and requires the canonical learned-data provenance, complete four-objective by five-seed archive, held-out/OOD evaluation, communication-aware ablations, packet evaluation, statistics, and its own immutable publication package.

## 7. Repository synchronization performed in final audit branch

The final audit branch synchronizes the Paper-1 README, frozen protocol, Markdown manuscript, completion audit, and publication manifest to the corrected evidence. Historical pre-correction files may remain only when explicitly labeled as historical provenance.

The canonical LaTeX manuscript already reflects the corrected holdout result and deliberately retains non-invented author metadata placeholders.

## 8. Remaining submission gates

The scientific evidence and manuscript narrative are corrected. External submission still requires:

- final CI and LaTeX/PDF build on the final synchronized branch head;
- visual/content audit of the resulting PDF;
- real author, affiliation, city/country, and email metadata;
- final venue-specific formatting and submission metadata if applicable.

These items must not be fabricated.

## Final status

**PASS WITH HUMAN/EXECUTION BLOCKERS.**

Corrected primary evidence exists and the scientific narrative can be synchronized without inventing results. The remaining blockers are final branch-head execution/build verification, final PDF inspection, and human author/submission metadata. Paper 1 remains a synthetic/model-based mechanism study, not externally measured validation.
