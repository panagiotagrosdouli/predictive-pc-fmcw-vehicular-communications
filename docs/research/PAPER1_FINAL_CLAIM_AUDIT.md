# Paper 1 Final Claim-to-Evidence Audit

**Audit date:** 2026-09-15  
**Base:** main `97f82ea816d5a8b10272c9e195fd8189b41b6ece` plus the publication-audit branch changes.  
**Scope:** corrected Paper 1 only.

## Headline claims and evidence

| Claim | Evidence source | Tier | Status |
|---|---|---|---|
| Physical packet deadlines use inclusive last-service slot `arrival + N - 1` and reject non-integral durations | `src/predictive_pc_fmcw/traffic.py`, deadline regression tests, `configs/paper1_final_protocol.json` | Implementation / protocol | Supported |
| Deployable prediction is causal; future ground truth is evaluator-only | `src/predictive_pc_fmcw/simulation/engine.py`, scheduler/oracle separation tests/docs | Implementation | Supported |
| Selected corrected policy is `service_guarded_100` with guard ratio 1.0 | `artifacts/paper1_final/primary_statistics.json`, frozen protocol | Corrected primary | Supported |
| Four corrected goodput deltas are 0.00000, +0.00035, -0.00050, +0.00080 Mbps | `artifacts/paper1_final/primary_statistics.json` | Corrected primary | Supported |
| All four corrected classifications are `NEUTRAL_OR_UNCERTAIN`; Holm-adjusted p-values are 1.0 | `artifacts/paper1_final/primary_statistics.json` | Corrected primary | Supported |
| Most corrected holdout comparisons are exact ties, limiting actionability of the selected guard | primary artifact plus manuscript | Primary + interpretation | Supported with descriptive wording |
| Prediction can change decisions without necessarily improving packet utility | frozen mechanism protocol + executed decision audit artifact | Diagnostic/mechanistic | Must remain conditional on observed audit |
| Strict service guarding can suppress predictive reordering | development selection + mechanism audit | Diagnostic/mechanistic | Conditional; not a universal law |
| The oracle quantifies value of future information under simulator assumptions | oracle scheduler implementation + decision audit | Diagnostic/oracle | Supported only as evaluator-only reference |
| The operating-region boundary is fully mapped | No frozen grid beyond four predeclared regimes | — | **Do not claim.** State that a full operating-region map was not executed. |
| Forecast-quality curves establish communication value versus error | No defensible frozen forecast-noise protocol | — | **Do not claim.** State as limitation. |
| Real-world optical validation exists | No measured optical channel or hardware-in-loop validation | — | **Do not claim.** |
| Paper 2/WOMD learned evidence validates the method | Learned evidence is outside Paper-1 scope and incomplete | — | **Do not claim.** |

## Forbidden stale claims

The following must not appear as current Paper-1 evidence:

- 3-of-4 improvement;
- `service_guarded_80` as the corrected selected policy;
- the 0.05 s deadline as a corrected regime;
- any statement that the corrected scheduler improves performance in three regimes;
- any universal predictive-superiority claim;
- any "first", "novel", "SOTA", or "state-of-the-art" claim without a bounded literature proof;
- any deployment claim based on the oracle;
- any statement that the simulator is measured-channel validated.

Historical `service_guarded_80` / 0.05 s material may be retained only when clearly marked as pre-correction provenance and never as corrected inference.

## Statistical unit audit

The confirmatory unit is the paired holdout scenario/episode seed: 20 disjoint pairs per regime. Slots and packets are outcomes within an episode, not independent inferential samples. Diagnostic analyses use their frozen five-seed paired episodes descriptively/mechanistically.

## Provenance audit

Corrected primary provenance:

- workflow run: `34785876008`
- head SHA: `2e3f48a3fa7597371d1fcb8ef505f40e2c52a1a1`
- artifact ID: `10326910705`
- artifact name: `prospective-current-service-guard`
- digest: `sha256:10ad8a88f4d8fa25216603b5e06171a464ab706adb9421793a3742b177127407`
- analysis: `scripts/14_analyze_service_guard_holdout.py`
- inferential pairs: 20 per regime
- bootstrap: 100,000 paired resamples; seed `20260914`

Historical pre-correction provenance remains separate:

- workflow run: `34055071988`
- artifact ID: `9995724323`
- selected policy: `service_guarded_80`
- invalid corrected regime: `deadline_0p05`

The historical artifact is not a source for current numerical claims.

## Release gate

This audit is complete only after the exact final commit passes CI and Paper-1 LaTeX, the post-merge corrected decision-audit workflow succeeds, stale-language search is clean or explicitly historical, and the final PDF artifact is available for visual inspection. Author/affiliation/email placeholders remain a human-only submission blocker until verified metadata is supplied.
