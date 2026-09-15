# When Does Trajectory Prediction Help PC-FMCW/DPSK Vehicular Optical Scheduling?

**Panagiota Grosdouli**  
Department of Electrical and Computer Engineering, Democritus University of Thrace, Xanthi, Greece  
Email: panagros1@ee.duth.gr

## Abstract

Predictive scheduling is often motivated by the intuition that future vehicle motion reveals communication opportunities before a reactive scheduler can observe them. This paper tests that claim for a model-based PC-FMCW/DPSK vehicular optical link without assuming that prediction is universally beneficial. We implement a strictly causal chain from observed vehicle history to trajectory prediction, future relative geometry, predicted link quality, packet queues and deadlines, scheduling, and realized packet-level outcomes. During final audit, an inclusive packet-deadline discretization defect was identified and corrected. The current-service guard was then prospectively re-selected on fresh development seeds and evaluated once on a disjoint 20-seed synthetic holdout. The corrected development protocol selected a 1.0 guard. Across four predeclared holdout regimes—0.1 s and 0.5 s deadlines, offered load 1.1, and +3 dB reference SNR—all primary goodput comparisons against Reactive Greedy are NEUTRAL_OR_UNCERTAIN under the frozen practical-margin/95% CI rule. The corrected evidence therefore does not support the historical pre-correction 3/4-improvement headline. Instead, it shows that protecting immediate service opportunity can make the selected predictive scheduler behave almost reactively at packet level. The optical channel is an analytical PC-FMCW/DPSK-informed simulation model; no measured optical-link or real-world vehicular validation is claimed.

## 1. Introduction

PC-FMCW laser-headlamp concepts can combine sensing, illumination, and DPSK communication. A mobility-aware scheduler raises a system-level question: should a receiver be served now because predicted future geometry indicates that its communication opportunity is about to degrade or disappear?

A reactive scheduler sees current link quality. A predictive scheduler can estimate future relative range and bearing and therefore future modeled SNR, BER/PER, goodput, outage, and link lifetime. Such information can be actionable near field-of-view, deadline, and link-loss boundaries, but forecast-driven urgency can also sacrifice a strong current transmission opportunity.

Accordingly, Paper 1 asks when and why causal future-motion/link information changes packet-level scheduling relative to reactive scheduling. The contribution is a reproducible mechanism study, not a universal prediction-gain claim.

## 2. Related Work and Novelty Boundary

This work lies at the intersection of vehicular optical communication, trajectory forecasting, predictive resource scheduling, and integrated sensing/communication. Prior work already applies trajectory prediction to dynamic VLC beam alignment/tracking and prior vehicular-VLC work studies resource utilization, connectivity, load balancing, and network lifetime. Paper 1 therefore makes no categorical first-of-kind claim for trajectory prediction, predictive scheduling, deadline-aware resource allocation, PC-FMCW, phase coding, or vehicular optical communication.

The narrower contribution is an auditable causal interface from motion forecasting to a PC-FMCW/DPSK-informed packet scheduler, with realized packet outcomes evaluated on ground-truth-derived link state while deployable policies remain causal.

## 3. System Model

At decision slot t, the scheduler observes vehicle histories through t, packet queues, deadlines, and past service. A causal predictor produces future target positions over horizon H. Ego-relative range and bearing are mapped through the modeled optical link to future SNR, BER/PER, goodput, outage, and link-lifetime estimates.

Realized packet outcomes use ground-truth-derived geometry at the current transmission slot. Forecasts affect decisions; they do not replace the realization model. Packet arrivals, deadlines, queue evolution, failed retransmissions, drops, and remaining right-censored packets obey queue-conservation checks.

The Part-A physical-layer reference is frozen separately. It supplies the PC-FMCW/DPSK premise and reference parameters, while the end-to-end geometry-to-link mapping remains an analytical simulation assumption. Absolute received power is not presented as measured/calibrated watts.

## 4. Problem Formulation and Proposed Method

For receiver i, a predictive scheduler evaluates a utility combining current/future modeled service, queue and deadline pressure, fairness/opportunity terms, and predicted link evolution:

`i* = argmax_i U_i(history_t, queue_t, deadlines_t, predicted_link_{t+1:t+H})`.

Link-lifetime urgency increases priority when a currently usable receiver is predicted to lose service. Diagnostics exposed a failure mode in which future urgency can reorder service away from a stronger current opportunity, especially under congestion.

The current-service guard permits predictive reordering only when the candidate preserves a specified fraction of immediate service opportunity. After correcting deadline semantics, the guard family was re-selected prospectively using fresh development seeds. The frozen corrected-development choice is `service_guarded_100`, guard ratio 1.0. This is a strong constraint: under the guard definition, predictive reordering cannot accept a lower immediate service score than the reactive choice.

## 5. Baselines and Information References

Reactive baselines include Random, Round Robin, Reactive Greedy, and Proportional Fair. Classical predictive methods use causal Last Position, constant-velocity, constant-acceleration, Kalman-CV, and IMM-style motion information where configured, together with predictive utility and link-lifetime scheduling. Oracle uses perfect future positions only as an evaluator-side information reference; it is not deployable and is not a globally optimal offline scheduler.

Paired comparisons share scenarios, traffic traces, deadlines, and transmission random numbers. Future ground truth never enters a deployable scheduler decision.

## 6. Corrected Experimental Protocol

The September 2026 audit found that an N-slot physical deadline had been encoded with inclusive last-service index `arrival + N`, permitting N+1 service opportunities. The corrected simulator uses `arrival + N - 1`. Physical deadlines must be exactly representable by the simulator slot duration; consequently, the historical 0.05 s regime is invalid at 0.1 s/slot and is retained only as pre-correction provenance.

Corrected development uses seeds 20270101--20270110 and corrected holdout uses disjoint seeds 20270201--20270220. Four regimes are predeclared: deadline 0.1 s, deadline 0.5 s, offered load 1.1, and reference SNR +3 dB. The primary endpoint is paired candidate-minus-Reactive goodput, with 20 paired episode/seed observations per holdout regime. Packets and time samples are not independent inferential units.

The analysis uses 100,000 paired percentile bootstrap replicates, a 95% confidence interval for the mean paired difference, a two-sided paired Wilcoxon signed-rank test, Holm correction over four primary comparisons, paired Cohen dz, and win/loss/tie fractions. With practical margin m = 0.001 Mbps, HELP requires the CI lower bound to exceed +m, HURT requires the CI upper bound to be below -m, and all other cases are NEUTRAL_OR_UNCERTAIN.

## 7. Corrected Confirmatory Results

The corrected development selection chose `service_guarded_100`. On the fresh holdout, none of the four primary comparisons establishes HELP or HURT under the frozen rule.

| Regime | Delta goodput (Mbps) | 95% paired bootstrap CI | Holm p | Cohen dz | Classification |
|---|---:|---:|---:|---:|---|
| deadline 0.1 s | +0.00000 | [0.00000, 0.00000] | 1.000000 | 0.000 | NEUTRAL_OR_UNCERTAIN |
| deadline 0.5 s | +0.00035 | [0.00000, 0.00105] | 1.000000 | 0.224 | NEUTRAL_OR_UNCERTAIN |
| offered load 1.1 | -0.00050 | [-0.00455, 0.00285] | 1.000000 | -0.060 | NEUTRAL_OR_UNCERTAIN |
| reference SNR +3 dB | +0.00080 | [-0.00080, 0.00255] | 1.000000 | 0.208 | NEUTRAL_OR_UNCERTAIN |

At the 0.1 s deadline all 20 paired differences are exact ties. At 0.5 s, 95% of pairs tie and 5% favor the guarded policy. At load 1.1, 85% tie, 10% favor and 5% disfavor it. At +3 dB, 80% tie, 15% favor and 5% disfavor it. Thus the corrected selected policy behaves very similarly to Reactive Greedy in these regimes.

## 8. Statistical Interpretation and Trade-offs

The confirmatory conclusions use episode-level paired inference. For the all-zero 0.1 s contrast, the Wilcoxon statistic is degenerate; the corrected summary records the raw test as undefined and conservatively uses Holm-adjusted p = 1. The other raw Wilcoxon p-values are 0.3173, 1.0, and 0.2733 for 0.5 s, load 1.1, and +3 dB respectively; all Holm-adjusted values are 1.0.

These results should not be interpreted as proof that the policies are identical. They show that, under the frozen practical-margin and uncertainty rule, the corrected holdout does not establish a robust incremental goodput advantage or harm for the selected guarded policy.

Less restrictive guards produced larger positive changes in some development regimes but failed the predeclared worst-regime noninferiority gate. The only eligible corrected-development candidate was the 1.0 guard, which then produced mostly ties on holdout. Development gains and historical pre-correction gains are therefore not promoted to confirmatory claims.

## 9. Ablations, Robustness, and Failure Modes

Corrected development diagnostics expose the service-order trade-off. Guard 0.8 showed positive development mean goodput at 0.5 s and +3 dB but a negative mean at the 0.1 s deadline, making it ineligible under the frozen rule. Guards 0.9 and 0.95 also failed the worst-regime noninferiority requirement. Guard 1.0 was eligible and selected before holdout inspection.

This pattern supports a mechanism conclusion rather than a superiority conclusion: future-link urgency can create opportunities, but the reordering cost needed to exploit them can violate performance constraints elsewhere. A sufficiently strict current-service guard suppresses that downside and, in the corrected holdout, also suppresses most incremental benefit.

## 10. Discussion

The corrected evidence changes the interpretation relative to the historical pre-correction run. The defensible conclusion is not that prediction improves three of four regimes. Under corrected packet timing and the prospectively selected robust guard, no predeclared holdout regime establishes a practically positive or negative goodput effect. This null/mixed result is retained rather than optimized away.

The result also shows why trajectory accuracy and future-link information cannot be equated with communication utility. A forecast can contain useful future geometry while a scheduler constrained to protect immediate service has little room to change packet ordering. Relaxing that constraint can expose both gains and losses across regimes.

## 11. Limitations

The confirmatory holdout is synthetic. The optical link is model-based and uses reference-SNR/geometry assumptions rather than measured end-to-end vehicle optical calibration. The Part-A waveform work provides physical-layer provenance but does not validate the scheduler's geometry-to-link model. No road deployment, hardware-in-the-loop experiment, or measured vehicular optical channel is claimed.

The study evaluates a finite set of predeclared operating regimes and a finite guard family. The selected 1.0 guard is not claimed globally optimal. Oracle is an information reference rather than an offline global optimum. Learned GRU/WOMD results are excluded because their complete frozen evidence belongs to Paper 2. Stronger external validation and broader operating-region coverage are required before general claims about predictive scheduling benefit.

## 12. Conclusion

After correcting packet-deadline discretization and repeating prospective development selection on fresh seeds, the robust current-service guard selected by the frozen rule is 1.0. On a disjoint 20-seed synthetic holdout, all four predeclared goodput comparisons against Reactive Greedy are NEUTRAL_OR_UNCERTAIN. The main scientific conclusion is therefore conditional and mechanism-focused: future motion/link information does not by itself guarantee packet-level value, and protecting current service can make a predictive scheduler effectively reactive in realized utility. Less constrained predictive reordering may expose gains in some regimes but also losses in others.

## 13. Reproducibility and Claim Boundary

The corrected evidence was produced by workflow run 34785876008 at source SHA `2e3f48a3fa7597371d1fcb8ef505f40e2c52a1a1`, artifact ID 10326910705, artifact name `prospective-current-service-guard`, digest `sha256:10ad8a88f4d8fa25216603b5e06171a464ab706adb9421793a3742b177127407`. Historical pre-correction evidence is retained for provenance but is not final inference. Paper-1 claims are limited to model-based/synthetic evidence and must not be described as measured optical or real-world vehicular validation.