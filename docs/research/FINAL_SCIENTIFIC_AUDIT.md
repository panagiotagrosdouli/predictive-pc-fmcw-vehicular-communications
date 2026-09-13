# Final Scientific Audit

Audit base: `main` at `9e57ced0036300c90fddb9a4b5f155142a7f8e50`.

Status: **CORRECTED-MODEL REVALIDATION IN PROGRESS.** This is not yet a declaration of final publication readiness.

Paper 1 and Paper 2 remain separate scopes. Paper 1 is a model-based/synthetic mechanism and operating-region study; Paper 2 remains incomplete until its learned checkpoint, held-out/OOD, downstream packet, statistics, and provenance gates are satisfied.

## Verified baseline

- Main CI run `34716692874` passed lint, 233 tests plus 20 subtests, stage-entrypoint checks, scientific validation, and Paper-1 LaTeX compilation.
- The same CI log correctly reports legacy combined WOMD/learned stages as blocked by missing external data/checkpoints. Green CI therefore does not imply Paper-2 publication readiness.
- Part-A provenance explicitly states that the supplied reference notebook was not locally rerun, the local link uses a reference-SNR abstraction, absolute received power is not calibrated, and no measured optical channel is claimed.
- The deployable scheduling path was inspected: causal forecast modes use history only; Oracle is a distinct forecast mode and `OracleScheduler` refuses a non-oracle context. Realized packet success uses current ground-truth-derived link state, while forecast information affects the decision only.

## Historical Paper-1 evidence reanalysis

The original service-guard artifact from workflow run `34055071988`, artifact `9995724323`, digest `sha256:041e93b097a21924fe3d7b37e4eeb6aaf8d54e1e2ff55f97f419bd81dac758df`, was downloaded during this audit before expiry.

The raw artifact contains exactly 200 development rows and 80 holdout rows. Independent recomputation from the 80 raw holdout rows reproduces the versioned regime-level mean differences, 100,000-resample paired percentile bootstrap intervals, paired Wilcoxon p-values, Holm adjustments, paired Cohen dz values, and win/loss/tie fractions. The historical statistical summary is therefore internally reproducible.

## Scientific defect found: packet deadline semantics

A real model defect was found in `src/predictive_pc_fmcw/traffic.py`.

Historically, a physical deadline converted to `N` slots was stored as `arrival_slot + N`, while queue expiration treated `deadline_slot` as an inclusive last-service slot (`deadline_slot < current_slot` expires). This gave every packet `N+1` possible service slots. For example, a nominal 0.5 s deadline at 0.1 s/slot could remain serviceable for six slots (up to 0.6 s latency), not five.

The historical `deadline_0p05` regime was additionally unrepresentable because 0.05 s is below the 0.1 s simulator slot duration and was silently clamped to one slot.

### Correction

- Physical deadlines must now equal an integer number of simulator slots; otherwise generation fails closed instead of silently rounding.
- An `N`-slot deadline now uses inclusive last-service index `arrival + N - 1`, permitting exactly `N` service slots including the arrival slot.
- Regression tests cover physical-duration invariance, rejection of nonrepresentable deadlines, and one-slot expiration behavior.
- The corrected tight-deadline regime is 0.1 s.
- Fresh corrected-model development seeds are `20270101`–`20270110`; fresh holdout seeds are `20270201`–`20270220`. Historical service-guard seeds are not reused.
- Historical run `34055071988` is retained as pre-correction provenance only. Its values must not be copied into final corrected-model claims.

Because this defect changes packet timing, it can change scheduler selection, goodput, latency, PDR, and downstream classifications. Full service-guard development selection and holdout inference must therefore be rerun.

## Literature and novelty audit

The original Paper-1 LaTeX bibliography had only two entries. A verified reference set has been added covering vehicular VLC, PC-FMCW waveform/transceiver prior art, coherent PC-FMCW radar, the optical PC-FMCW laser-headlamp premise, reliability/latency-aware vehicular allocation, trajectory-prediction-assisted vehicular resource decisions, predictive resource allocation, and IMM trajectory forecasting. See `docs/research/REFERENCE_VERIFICATION.md`.

Novelty must be comparative and narrow. The repository does not establish first use of trajectory prediction, predictive scheduling, deadline-aware vehicular allocation, PC-FMCW, phase coding, or vehicular optical communication. The defensible contribution is the causal trajectory→link→packet mechanism study, explicit service-order trade-off, and evidence-backed operating-region characterization.

## Additional claim cleanup

The `LinkModel` code-level documentation previously called the geometry link abstraction “calibrated” even though configuration and publication text state that absolute received power is not calibrated. The docstring now uses “reference-SNR-anchored” wording; numerical behavior is unchanged.

`artifacts/audit/repository_inventory.md` is historical Stage-0 audit provenance tied to old SHAs and a 71-test baseline. It must not be interpreted as the current readiness record; this document is the current audit record.

## Remaining final gates

1. Execute the frozen corrected service-guard workflow and inspect its raw artifact and statistical analysis.
2. Update `artifacts/paper1_final/primary_statistics.json`, publication manifest, manuscript abstract/results/conclusion, completion audit, README/status documents, and any tables strictly from corrected evidence.
3. Run current CI and Paper-1 LaTeX on the final branch revision; inspect the generated PDF for unresolved citations/references and layout failures.
4. Verify no stale pre-correction numbers or `deadline_0p05` claims remain in publication-facing text except explicitly historical provenance.
5. Replace author/affiliation/email placeholders with real supplied metadata before external submission.

## Acceptance rules

Preserve negative/null findings; never relabel simulation as measurement; never use future ground truth in deployable decisions; keep scenario/episode-level inference where frozen; never use test/OOD data for selection; never call Paper 2 ready without the actual learned evidence; and require every final headline claim to be traceable to executed corrected evidence.
