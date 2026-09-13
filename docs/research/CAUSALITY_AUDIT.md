# Causality Audit — Paper 1

The deployable scheduler path was inspected at the code level.

- `run_simulation` constructs the current realized link from the ground-truth geometry at the current slot.
- Predictive forecast modes receive only combined positions through the current time index; sensing/history noise is applied only to the observed past for non-reactive/non-oracle modes.
- Classical predictors extrapolate from causal history. The learned forecast interface, when used, consumes a truncated causal relative-history window and is outside Paper-1 claims.
- Oracle is a distinct `forecast_mode="oracle"`; `OracleScheduler.select` raises unless the context is marked as an oracle forecast.
- The same current realized link is used for packet-success realization regardless of scheduler. Forecasts affect selection, not the packet realization law.
- Paired scheduler comparisons reuse deterministic seed-defined scenarios, traffic traces, and transmission-success uniforms.

No direct future-ground-truth path into a deployable Paper-1 scheduler decision was identified in this audit. This statement is about the inspected implementation and does not convert Oracle into a deployable method or global optimum.
