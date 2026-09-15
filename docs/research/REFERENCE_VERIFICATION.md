# Reference Verification — Paper 1

Status: verified bibliography set for the Paper-1 positioning audit. This file records what each citation may safely support; it is not a novelty claim by itself.

| Key | Verified source | DOI | Safe use in Paper 1 |
|---|---|---|---|
| `memedi2021vehicular` | A. Memedi and F. Dressler, *Vehicular Visible Light Communications: A Survey*, IEEE Communications Surveys & Tutorials 23(1), 161–181 | 10.1109/COMST.2020.3034224 | Vehicular VLC context, directionality/alignment/mobility challenges. |
| `jiang2020trajectory` | W. Jiang, X. Jin, Y. Zhang, M. Jin, C. Gong, and Z. Xu, *Trajectory Prediction of Target Light Source for Dynamic Visible Light Communication Systems with A Narrow Field of View*, IEEE ICC Workshops 2020 | 10.1109/ICCWorkshops49005.2020.9145246 | Direct prior art for trajectory prediction in dynamic narrow-FoV vehicular VLC. |
| `msongaleli2020resource` | D. L. Msongaleli and K. Kucuk, *Optimal Resource Utilisation Algorithm for Visible Light Communication-Based Vehicular Ad-Hoc Networks*, IET Intelligent Transport Systems 14(2), 65–72 | 10.1049/iet-its.2019.0224 | VLC-VANET resource allocation using lifetime, connectivity, and load balancing. |
| `gao2023imm` | H. Gao et al., *An Interacting Multiple Model for Trajectory Prediction of Intelligent Vehicles in Typical Road Traffic Scenario*, IEEE TNNLS 34(9), 6468–6479 | 10.1109/TNNLS.2021.3136866 | IMM-style vehicle trajectory forecasting prior art. |
| `kumbul2023smoothed` | U. Kumbul et al., *Smoothed Phase-Coded FMCW: Waveform Properties and Transceiver Architecture*, IEEE TAES 59(2), 1720–1737 | 10.1109/TAES.2022.3206173 | PC-FMCW waveform/transceiver prior art; phase coding is not novel here. |
| `kumbul2023mimo` | U. Kumbul et al., *Phase-Coded FMCW for Coherent MIMO Radar*, IEEE TMTT 71(6), 2721–2733 | 10.1109/TMTT.2022.3228950 | Experimentally evaluated PC-FMCW radar architecture; no claim that this repo invented PC-FMCW. |
| `liu2026laserheadlamp` | S. Liu, T. Sun, X. Shu, J. Song, and Y. Dong, *Phase-Coded FMCW Laser Headlamp for Integrated Sensing, Communication, and Illumination*, IEEE Photonics Technology Letters 38(14), 1032–1035 | 10.1109/LPT.2025.3649597 | Direct optical vehicular PC-FMCW/ISCAI premise; Paper 1 is a downstream scheduling/model study. |
| `guo2019latency` | C. Guo, L. Liang, and G. Y. Li, *Resource Allocation for Vehicular Communications With Low Latency and High Reliability*, IEEE TWC 18(8), 3887–3902 | 10.1109/TWC.2019.2919280 | Reliability/latency-aware vehicular resource allocation prior art. |
| `hajrasouliha2021trajectory` | A. Hajrasouliha and B. Shahgholi Ghahfarokhi, *Dynamic Geo-Based Resource Selection in LTE-V2V Communications Using Vehicle Trajectory Prediction*, Computer Communications 177, 239–254 | 10.1016/j.comcom.2021.08.006 | Trajectory-prediction-assisted V2V resource selection and PRR/blocking evaluation. |
| `guo2022trajectoryoffload` | H. Guo, L.-l. Rui, and Z.-p. Gao, *V2V Task Offloading Algorithm with LSTM-based Spatiotemporal Trajectory Prediction Model in SVCNs*, IEEE TVT 71(10), 11017–11032 | 10.1109/TVT.2022.3185085 | Trajectory-prediction-assisted vehicular communication/resource decisions. |
| `lu2024predictive` | B. Lu, B. Fan, Y. Wu, L. P. Qian, H. Zhang, and R. Lu, *Predictive Computation Offloading and Resource Allocation in DT-Empowered Vehicular Networks*, IEEE T-ITS 25(6), 5474–5487 | 10.1109/TITS.2023.3331885 | Predictive vehicular offloading/resource-allocation prior art. |
| `yin2026mobilityaware` | Y. Yin et al., *Mobility-Aware Assisted Deep Reinforcement Learning for Collaborative Task Migration and Resource Allocation in Vehicular Edge Computing*, IEEE TVT 75(7), 14681–14694 | 10.1109/TVT.2026.3660321 | Current prior art combining trajectory prediction with proactive vehicular resource decisions. |

## Claim boundary

The literature does not support claims that trajectory prediction, predictive scheduling/resource allocation, deadline/reliability-aware vehicular allocation, phase coding, PC-FMCW, or vehicular optical communication is new in itself. Paper 1 must not use unsupported "first", "novel", "state of the art", or "outperforms" language as a novelty claim.

The defensible contribution is narrower: a causal trajectory→link→packet evaluation of a PC-FMCW/DPSK-informed directional optical scheduler, explicit separation of forecast information from scheduler disagreement and realized packet utility, and mechanism analysis of the service-order constraint that can suppress incremental predictive actionability. The corrected primary result remains null/mixed across all four predeclared regimes.

Publisher/institutional metadata was checked during the September 2026 audit. New references must be verified by title, authors, venue, year/pages, DOI, and the exact manuscript proposition they support. The literature matrix in `docs/research/LITERATURE_EVIDENCE_MATRIX.md` records the broader comparison dimensions.
