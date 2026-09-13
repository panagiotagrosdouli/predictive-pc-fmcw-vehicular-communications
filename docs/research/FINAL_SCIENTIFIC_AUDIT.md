# Final Scientific Audit

Audit base: `main` at `9e57ced0036300c90fddb9a4b5f155142a7f8e50`.

Status: **IN PROGRESS**. This is not a declaration of publication readiness.

Paper 1 and Paper 2 remain separate scopes. Paper 1 is a model-based/synthetic mechanism and operating-region study; Paper 2 remains incomplete until its learned checkpoint, held-out/OOD, downstream packet, statistics, and provenance gates are satisfied.

## Initial findings

- Latest observed main CI at the audit base is green.
- No open pull requests were present at audit start.
- Paper-1 frozen evidence reports `service_guarded_80` versus `reactive_greedy`, with 20 paired holdout seeds per regime, 100,000 paired bootstrap replicates, Wilcoxon tests, Holm correction, and paired Cohen dz. These statistics still require independent raw-evidence verification.
- The Paper-1 LaTeX bibliography currently has only two entries and requires a real primary-source literature/novelty audit before stronger external-publication positioning.
- `artifacts/audit/repository_inventory.md` is historical Stage-0 provenance tied to old SHAs and must not be read as current publication status.
- Part-A provenance says the reference notebook was not locally rerun, the local link uses a reference-SNR abstraction, received power is normalized rather than calibrated watts, and no measured optical channel is claimed.

## Acceptance rules

Preserve negative/null findings; never relabel simulation as measurement; never use future ground truth in deployable decisions; keep scenario/episode-level inference where frozen; never use test/OOD data for selection; never call Paper 2 ready without the actual learned evidence; and require every final headline claim to be traceable to executed evidence.