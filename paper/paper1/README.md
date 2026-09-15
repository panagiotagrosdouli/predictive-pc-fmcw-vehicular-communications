# Paper 1 — Mechanism / Operating-Region Study

**Scope label:** `PAPER1`

**Title:** *When Does Trajectory Prediction Help PC-FMCW/DPSK Vehicular Optical Scheduling?*

Paper 1 is the self-contained classical/mechanism Part-B study. Reusable implementation remains under `src/predictive_pc_fmcw/`; this directory contains publication-facing protocol and manuscript material.

## Research question

When does causal future-motion/link information have real packet-level scheduling value, when does it become neutral or harmful, and why?

## Proposed method

The Paper-1 method is predictive communication-aware scheduling with a prospectively selected **current-service guard**. Future-link urgency may reorder service only while preserving a specified fraction of current modeled service opportunity.

After the September 2026 packet-deadline correction, the prospective development protocol was repeated on fresh development seeds and selected `service_guarded_100`, guard ratio 1.0. This strict guard protects immediate service opportunity and leaves little room for predictive reordering.

## Corrected evidence boundary

The canonical corrected Paper-1 evidence is the fresh prospective synthetic holdout produced by workflow run `34785876008` at SHA `2e3f48a3fa7597371d1fcb8ef505f40e2c52a1a1`, artifact `10326910705`, digest `sha256:10ad8a88f4d8fa25216603b5e06171a464ab706adb9421793a3742b177127407`.

Development seeds are `20270101`--`20270110`; holdout seeds are the disjoint set `20270201`--`20270220`. The corrected regimes are deadline 0.1 s, deadline 0.5 s, offered load 1.1, and reference SNR +3 dB.

All four corrected primary goodput comparisons against Reactive Greedy are **NEUTRAL_OR_UNCERTAIN** under the frozen +/-0.001 Mbps practical-margin and 95% CI rule. The corrected result therefore does not support the historical pre-correction claim that the guarded predictive policy improves three of four regimes.

The historical run `34055071988`, `service_guarded_80`, the 0.05 s deadline regime, and the historical 3/4 HELP statistics remain immutable pre-correction provenance only.

The optical channel is model-based. No measured optical-link, road deployment, hardware-in-the-loop, or real-world vehicular validation is claimed.

## Frozen protocol

`manifests/PAPER1_FINAL_PROTOCOL.md` defines the corrected research question, deadline correction, causal/fairness constraints, independent experimental unit, confirmatory comparison, statistical procedure, claim boundary, and Paper-1/Paper-2 separation.

`configs/paper1_final_protocol.json` records the machine-readable corrected protocol. `artifacts/paper1_final/primary_statistics.json` is the publication-facing corrected primary statistical summary.

## Manuscript

`manuscript/main.tex` is the canonical typeset manuscript. It uses only the corrected primary results for its headline inference. `manuscript/PAPER1_FINAL_DRAFT.md` must remain synchronized with it and must not contain historical pre-correction headline claims.

## Paper-2 boundary

Incomplete GRU/WOMD learned-model claims are excluded from Paper 1. The four-objective, five-seed learned study belongs to Paper 2 and is not required for the university Part-B Paper-1 mechanism contribution.

## Reproducibility rule

Corrected publication artifacts belong under `artifacts/paper1_final/`. Diagnostic or historical evidence must retain its exact evidence label and provenance. Individual packets or time samples must never be treated as independent statistical observations when the independent unit is the paired scenario/episode seed within regime.

## Current status

Paper 1 has corrected primary evidence and a synchronized LaTeX scientific narrative. The final submission gate still requires a final repository/manuscript build audit on the final synchronized branch head and replacement of deliberately non-invented author/affiliation/email placeholders before external submission.
