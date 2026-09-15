# Reviewer-2 Red-Team Audit — Paper 1

**Audit date:** 2026-09-15  
**Scope:** PAPER1 only  
**Evidence basis:** corrected primary statistics, frozen protocol, repository implementation/docs, verified literature matrix, and existing diagnostic infrastructure.

## Executive assessment

The paper is defensible if presented as a synthetic/model-based mechanism study with a null/mixed corrected primary result. It is not defensible as a universal predictive-scheduling improvement paper, a measured optical-channel validation paper, or a first-use novelty claim. The strongest contribution is methodological/mechanistic: future mobility information can exist without producing robust packet-level value when the scheduler constraint required for immediate-service robustness suppresses most predictive reordering.

## Criticisms and disposition

| Reviewer-2 concern | Assessment | Disposition |
|---|---|---|
| Is the contribution actually new? | Broad ingredients are established: vehicular VLC, trajectory prediction in VLC, trajectory-informed V2V allocation, predictive offloading/resource allocation, deadline/reliability-aware allocation, and PC-FMCW all have prior art. | Narrow novelty boundary to the cross-layer trajectory→link→packet actionability study and service-order mechanism. Avoid first/novel/SOTA language. |
| Is the paper just a negative result? | The corrected primary endpoint is null/uncertain in all four regimes, but the mechanism question is substantive and the diagnostic protocol distinguishes disagreement from packet utility. | Frame the paper around the condition under which future information becomes actionable, not around a failed improvement. Keep the null result visible. |
| Why should prediction help theoretically? | Future geometry can change predicted link quality/lifetime before current-state metrics reveal the same deterioration. | Explain the causal path, while emphasizing that predicted link urgency is not identical to packet urgency. |
| Why does it not help here? | The corrected selected guard is 1.0, so predictive reordering is heavily constrained. Existing ablations also show that removing prediction changes the scheduler while aggregate utility can remain close. | State as an evidence-matched mechanism interpretation, not as a universal causal law. |
| Is the oracle meaningful? | Yes as a non-deployable future-information evaluator under the simulator's assumptions. It is not a proof of global optimality. | Label it evaluator-only/value-of-information reference everywhere. |
| Is the simulator sufficiently realistic? | It is a model-based PC-FMCW/DPSK-informed optical simulation with synthetic mobility; absolute received power is not calibrated and no measured optical channel is claimed. | Retain explicit limitations and do not generalize to road deployment. |
| Are deadlines implemented correctly? | Corrected implementation uses `arrival_slot + N - 1` for an N-slot inclusive deadline and rejects non-integral physical deadlines. | Treat this as a central correction; historical 0.05 s evidence is pre-correction only. |
| Is future information leaking into deployable policies? | The inspected simulation path separates causal predictor modes from the oracle; realized packet success uses current ground-truth-derived link state, while forecast information affects decisions. | Preserve the separation in methods and code audit. |
| Are statistical units correct? | Primary inference uses 20 paired holdout seeds per regime; slots and packets are not inferential replicates. | Keep paired-seed language explicit and avoid slot/packet significance claims. |
| Is the seed count adequate? | Twenty paired synthetic seeds are sufficient for the frozen analysis but do not justify broad external generalization. | Report the exact count and uncertainty; describe small diagnostic seed sets as descriptive/mechanistic. |
| Are claims broader than evidence? | A risk exists if diagnostic improvements or historical 3/4 results are promoted. | Current claim boundary forbids this. Audit stale claims before release. |
| Are prior works missing? | The literature audit now includes direct dynamic-VLC trajectory prediction, VLC-VANET resource allocation, LTE-V2V trajectory-informed allocation, predictive vehicular offloading/resource allocation, latency/reliability allocation, and 2026 mobility-aware edge resource allocation. | Maintain the evidence matrix and verified bibliography. |
| Does the mechanism analysis explain the primary result? | It can explain why a strict guard can remove actionability, but diagnostic disagreement alone cannot establish beneficial/harmful counterfactual packet causality because scheduler traces diverge after decisions. | Do not invent disagreement classifications without explicit counterfactual instrumentation. |
| Is the contribution useful when primary gains are null? | Yes: it gives a reproducible negative boundary condition and identifies the distinction between prediction accuracy, decision change, and packet utility. | Make this the principal discussion/conclusion value. |

## Specific scientific checks

### Deadline semantics

The corrected contract is: a physical deadline must equal an integer number of simulator slots; an N-slot deadline has last legal service index `arrival + N - 1`. The historical 0.05 s regime at `dt = 0.1 s` is not representable and must never appear as corrected evidence.

### Causality

Deployable predictors receive only observed history. Future ground truth may be used only by the explicit oracle/evaluator pathway. The oracle must not be described as a deployable policy or globally optimal scheduler.

### Primary evidence

The frozen corrected policy is `service_guarded_100` with guard ratio 1.0. The four primary paired goodput differences are:

- `deadline_0p1`: +0.00000 Mbps, CI [0, 0]
- `deadline_0p5`: +0.00035 Mbps, CI [0, 0.00105]
- `load_1p1`: -0.00050 Mbps, CI [-0.00455, 0.00285]
- `snr_plus3`: +0.00080 Mbps, CI [-0.00080, 0.00255]

All four are `NEUTRAL_OR_UNCERTAIN`; Holm-adjusted p-values are 1.0. No 3-of-4 improvement claim is permissible for corrected evidence.

### Anomaly handling

The repository history records an earlier Part-A BER anomaly that was traced to an FFT alias-branch inconsistency and corrected before the current canonical Stage-2 evidence. The corrected Stage-2 documentation explicitly removes the earlier paired 7→8 dB result from canonical evidence. Therefore the old anomaly is provenance, not a current Paper-1 headline result.

A separate forecast-error/history-noise diagnostic exists in corrected-v2 ablations. Its small, non-monotone changes are not sufficient to establish a causal forecast-quality relationship, and no arbitrary noise curve should be added to the paper.

## Reviewer-2 conclusion

The paper should be accepted as a bounded simulation/mechanism study only if it remains explicit about: (1) synthetic/model-based evidence, (2) corrected null/mixed primary results, (3) causal versus oracle information, (4) paired-seed inference, (5) established prior art, and (6) the inability of current traces to support unambiguous beneficial/harmful disagreement labels. The null result is not a defect to hide; it is part of the evidence boundary.
