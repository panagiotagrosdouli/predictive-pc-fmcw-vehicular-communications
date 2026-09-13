# Historical Raw-Evidence Reanalysis

Source: GitHub Actions run `34055071988`, artifact `9995724323`, name `prospective-current-service-guard`, digest `sha256:041e93b097a21924fe3d7b37e4eeb6aaf8d54e1e2ff55f97f419bd81dac758df`.

The artifact was downloaded during the September 2026 audit and contains `prospective_service_guard_selection.json` with exactly 200 development rows and 80 holdout rows. The stored development selection is `service_guarded_80` with guard ratio 0.8.

Independent re-execution of the frozen analysis formulae on the raw 80 holdout rows reproduces the versioned primary statistics to reported precision:

| regime | mean Δ goodput Mbps | 95% paired bootstrap CI | raw Wilcoxon p | Holm p | paired Cohen dz |
|---|---:|---:|---:|---:|---:|
| deadline_0p05 | 0.03730 | [0.02195, 0.05365] | 0.000624865 | 0.001874595 | 1.000498 |
| deadline_0p5 | 0.05680 | [0.04015, 0.07530] | 0.000131834 | 0.000527336 | 1.384365 |
| load_1p1 | 0.00860 | [-0.00230, 0.02050] | 0.295869342 | 0.295869342 | 0.321695 |
| snr_plus3 | 0.01915 | [0.00790, 0.03120] | 0.009976937 | 0.019953873 | 0.706319 |

This verifies statistical reproducibility of the historical artifact. It does **not** rescue those values as final evidence after the packet-deadline semantics defect was discovered. They remain pre-correction provenance and the corrected model must be re-executed on fresh disjoint seeds.
