# Statistical Audit — Paper 1

The frozen historical analysis uses one paired episode/seed difference per regime observation; packets and slots are not treated as independent inferential replicates. The analysis computes a paired percentile bootstrap of the mean difference, two-sided Wilcoxon signed-rank test, Holm correction across the four predeclared primary regime comparisons, paired Cohen dz, and win/loss/tie fractions.

The Holm implementation is monotone in sorted raw p-values and reproduces the historical adjusted values. Independent recomputation from the raw historical artifact also reproduces the reported confidence intervals and effect sizes. The statistical machinery itself is therefore not the reason historical results are superseded; they are superseded because the underlying packet-deadline simulation semantics changed.

The corrected analysis retains the same primary metric, practical margin, four-comparison Holm family, paired unit, and 100,000-resample interval procedure, but uses a new analysis RNG seed and fresh corrected development/holdout populations. Any selected guard and all corrected numerical results must come from the new artifact rather than being fixed to the historical `service_guarded_80` outcome.
