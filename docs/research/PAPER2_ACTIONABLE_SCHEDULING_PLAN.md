# Actionable Predictive Scheduling: Paper 2 Study Plan

## Research question
How can causal future-mobility information be converted into measurable packet-level gains in vehicular optical scheduling without sacrificing deadline reliability or fairness?

## Scientific premise
Paper 1 identifies an actionability bottleneck: future information can be informative while producing little incremental packet utility when the scheduler cannot safely change a consequential service decision. Paper 2 will test a scheduler designed specifically to resolve that bottleneck. Algorithm development, model selection, and confirmatory evaluation remain separated.

## Proposed scheduler
Working name: **Actionable Predictive Scheduler (APS)**.

At every service opportunity APS compares the best reactive action with forecast-driven alternatives using immediate service value, packet/deadline urgency, predicted loss of future optical opportunity, and forecast confidence. A predictive action is taken only when estimated incremental packet value exceeds its immediate opportunity cost by a calibrated decision margin. This replaces a fixed current-service guard with a state-dependent actionability test.

A generic development score is:

`APS(i) = immediate_value(i) + lambda * confidence(i) * future_opportunity_loss(i) + mu * deadline_urgency(i)`

Exact functional forms and parameters are development quantities and must be frozen before confirmatory evaluation.

## Baselines
Retain Random, Round Robin, Reactive Greedy, Proportional Fair, and the Paper-1 guarded predictive policy. An evaluator-only future-information reference may be used as an information benchmark, but is neither deployable nor globally optimal.

## Development protocol
Use development seeds disjoint from all confirmatory seeds. Implement APS and tests; verify queue/deadline conservation and strict causality; sweep only predeclared parameters; measure goodput, deadline-delivery ratio, expiration/drop rate, latency, fairness, scheduler disagreement, action-change rate, and conditional utility of changed actions; test forecast-error/uncertainty sensitivity; then freeze one configuration with a predeclared multi-metric selection rule.

Development results remain diagnostic and cannot be promoted to confirmatory evidence after inspection.

## Confirmatory protocol
After APS is frozen, evaluate once on a new untouched holdout. Primary comparison: APS minus Reactive Greedy on packet goodput. Secondary outcomes: deadline-delivery ratio, expiration/drop rate, latency, and fairness. Use paired scenario seeds, confidence intervals, multiplicity correction across predeclared primary regimes, paired effect sizes, and win/loss/tie fractions.

A positive conclusion requires more than a positive sample mean: the confidence interval must support a predeclared practically meaningful gain while reliability and fairness safety constraints remain satisfied. If this is not met, report the observed result without changing the holdout or acceptance rule.

## Mechanism measurements
Directly measure prediction-induced action-change rate, useful-action rate, harmful-action rate, conditional gain given an action change, forecast confidence at useful versus harmful changes, deadline slack, predicted link-opportunity loss, and a decomposition of total gain into action frequency and gain per consequential action.

## Operating-region design
Before confirmatory evaluation, build a development map spanning representable packet deadlines, offered load, reference SNR, mobility/link-lifetime stress, and forecast quality. Select confirmatory regimes from scientific hypotheses rather than from cells with the largest development gain. Include difficult regimes where predictive reordering can be harmful.

## Success criterion
The intended contribution is a scheduler that converts future-mobility information into statistically and practically supported packet-level benefit under identified actionability conditions. No numerical gain is assumed in advance. The study remains scientifically informative if the final effect is positive, conditional, or null.

## Paper narrative
**Problem:** prediction accuracy alone does not guarantee communication value.

**Paper-1 observation:** robust protection of immediate service can collapse predictive actionability.

**Paper-2 hypothesis:** a state-dependent, uncertainty-aware actionability gate can exploit future information only when expected packet-level benefit exceeds immediate opportunity cost.

**Evidence required:** a new algorithm, disjoint development/holdout evaluation, multi-metric safety checks, and direct decision-level mechanism measurements.
