# Paper 1 Literature Evidence Matrix

**Audit date:** 2026-09-15  
**Scope:** PAPER1  
**Purpose:** bounded literature positioning for the mechanism question, not a novelty claim by itself.

The matrix emphasizes prior work that already connects mobility/trajectory information to optical or vehicular communication decisions. Metadata was cross-checked against publisher, institutional, or bibliographic records where available. The closest-overlap column is deliberately comparative: trajectory prediction, mobility-aware allocation, deadline/reliability-aware allocation, and PC-FMCW/vehicular optical communication are established areas.

| Citation | Year | Communication domain | Prediction / mobility information | Scheduling / resource role | Packet / queue awareness | Future ground truth use | Evaluation setting | Closest overlap with Paper 1 | Remaining distinction |
|---|---:|---|---|---|---|---|---|---|---|
| Memedi & Dressler, *Vehicular Visible Light Communications: A Survey*, IEEE COMST | 2021 | Vehicular VLC | Mobility, geometry, alignment, channel constraints | Survey/context rather than a scheduler | Discusses communication-system constraints | N/A | Literature survey | Establishes the directional, mobility-sensitive vehicular VLC setting | Does not provide this paper's causal trajectory→link→packet scheduler experiment |
| Jiang et al., *Trajectory Prediction of Target Light Source for Dynamic VLC Systems with a Narrow Field of View*, IEEE ICC Workshops | 2020 | Vehicular VLC | Target/light-source trajectory prediction for narrow FoV alignment | Prediction is used to anticipate optical pointing opportunity | Not a packet-queue scheduler | Prediction is derived from available motion history; no future-truth deployment claim identified | Simulation/communication-oriented trajectory study | Directly demonstrates trajectory prediction in dynamic vehicular VLC | Focus is target trajectory/beam alignment and received optical intensity, not packet deadlines or scheduler utility |
| Msongaleli & Kucuk, *Optimal Resource Utilisation Algorithm for VLC-Based Vehicular Ad-Hoc Networks*, IET ITS | 2020 | VLC VANET | Vehicle position/direction and link lifetime considerations | Multi-objective ILP and heuristic for lifetime, connectivity, load balancing | Network-level traffic/load, not per-packet deadline scheduling | No oracle role comparable to this study | Numerical/simulation VANET | Directly establishes mobility-aware resource allocation in VLC VANETs | Does not trace causal forecast→scheduler disagreement→packet utility with paired episode inference |
| Guo, Liang & Li, *Resource Allocation for Vehicular Communications With Low Latency and High Reliability*, IEEE TWC | 2019 | RF V2V/V2N | Slowly varying large-scale fading information | Reliability/latency-aware power and spectrum allocation | Explicit reliability/latency constraints and queueing analysis | No future-ground-truth oracle role | Analytical + simulation | Establishes that vehicular allocation should be evaluated against latency/reliability, not channel quality alone | RF resource reuse/power allocation rather than optical mobility forecasting and packet service ordering |
| Hajrasouliha & Shahgholi Ghahfarokhi, *Dynamic Geo-Based Resource Selection in LTE-V2V Communications Using Vehicle Trajectory Prediction*, Computer Communications | 2021 | LTE-V2V | Deep-learning vehicle trajectory prediction and future density | Future density informs geographic resource-pool assignment | PRR/QoS outcomes, but not packet-queue/deadline service ordering | Uses predicted future positions; not a deployable future-ground-truth oracle | Highway/urban simulation | Very close precedent for trajectory prediction changing communication resource selection | Radio geo-based pool allocation, not optical link-state prediction or packet-level service urgency |
| Gao et al., *An Interacting Multiple Model for Trajectory Prediction of Intelligent Vehicles in Typical Road Traffic Scenario*, IEEE TNNLS | 2023 | Vehicle trajectory prediction | IMM/multiple motion hypotheses | Predictor prior art; not a communication scheduler | None | Causal forecasting method | Vehicle trajectory evaluation | Supports the classical causal IMM predictor used here | No communication/resource-allocation outcome layer |
| Guo, Rui & Gao, *V2V Task Offloading Algorithm with LSTM-based Spatiotemporal Trajectory Prediction Model in SVCNs*, IEEE TVT | 2022 | V2V / vehicular cooperative networks | LSTM spatiotemporal trajectory prediction | Predicted mobility informs task offloading/resource decisions | Task-service time/success, not packet deadline service | Prediction-based decision process; no evaluator-only oracle analogous to Paper 1 | NS-3 + trajectory-model simulation | Strong precedent for prediction-assisted vehicular communication decisions | Computation offloading in software-defined vehicular networks, not optical packet scheduling |
| Lu et al., *Predictive Computation Offloading and Resource Allocation in DT-Empowered Vehicular Networks*, IEEE T-ITS | 2024 | Vehicular networks / digital twins | Predicted V2V pairing and network-state updates | Prediction-based offloading, channel allocation, and update-frequency decisions | Communication/computation cost; not packet queue deadlines | Uses predicted network state, not a future-ground-truth deployment policy | Numerical simulation | Establishes predictive resource allocation in vehicular networks | Digital-twin/offloading objective differs from optical packet service ordering |
| Yin et al., *Mobility-Aware Assisted Deep Reinforcement Learning for Collaborative Task Migration and Resource Allocation in Vehicular Edge Computing*, IEEE TVT | 2026 | Vehicular edge / V2V-V2I | Mamba-based trajectory prediction and future spatiotemporal state | Prediction guides task migration and resource allocation | Task completion delay/workload balance, not packet deadline service | Forward-looking state is a model input; not the oracle/evaluator separation used here | Real-world Cologne trajectory dataset + simulation | Current close precedent for prediction-guided proactive vehicular resource decisions | Edge task migration and DRL rather than optical link prediction and packet-level scheduler actionability |
| Kumbul et al., *Smoothed Phase-Coded FMCW: Waveform Properties and Transceiver Architecture*, IEEE TAES | 2023 | PC-FMCW sensing/radar | N/A | N/A | N/A | N/A | Waveform/transceiver analysis | Establishes PC-FMCW waveform/transceiver prior art | Not vehicular packet scheduling |
| Kumbul et al., *Phase-Coded FMCW for Coherent MIMO Radar*, IEEE TMTT | 2023 | PC-FMCW radar | N/A | N/A | N/A | N/A | Experimental radar evaluation | Establishes PC-FMCW radar architecture prior art | Not optical packet scheduling |
| Liu et al., *Phase-Coded FMCW Laser Headlamp for Integrated Sensing, Communication, and Illumination*, IEEE Photonics Technology Letters | 2026 | Optical vehicular sensing/communication | N/A | Integrated optical platform rather than scheduler | Not packet scheduling | N/A | Optical hardware/experimental context | Directly motivates the PC-FMCW laser-headlamp premise | Paper 1 is a downstream model/scheduling study and does not claim measured-channel validation |

## Novelty boundary after audit

The literature does **not** support claims that trajectory prediction, predictive scheduling/resource allocation, deadline/reliability-aware vehicular allocation, vehicular VLC, or PC-FMCW is new in itself. The defensible boundary is narrower:

1. a reproducible causal interface from motion history to predicted optical-link evolution and packet scheduling;
2. explicit separation of forecast information, scheduler disagreement, and realized packet utility;
3. a corrected paired-seed holdout showing that the prospectively selected strict current-service guard yields no robust incremental primary goodput effect in the four frozen regimes; and
4. a mechanism interpretation in which the constraint that protects immediate service can simultaneously suppress the actionable benefit of future mobility information.

These are model-based/synthetic claims, not real-world or measured-optical validation claims.

## Verification notes

- Jiang et al.: DOI `10.1109/ICCWorkshops49005.2020.9145246`; IEEE ICC Workshops 2020.
- Msongaleli & Kucuk: DOI `10.1049/iet-its.2019.0224`; IET Intelligent Transport Systems 14(2), 65–72 (2020).
- Hajrasouliha & Shahgholi Ghahfarokhi: DOI `10.1016/j.comcom.2021.08.006`; Computer Communications 177, 239–254 (2021).
- Guo et al.: DOI `10.1109/TWC.2019.2919280`; IEEE TWC 18(8), 3887–3902 (2019).
- Guo et al. offloading: DOI `10.1109/TVT.2022.3185085`; IEEE TVT 71(10), 11017–11032 (2022).
- Lu et al.: DOI `10.1109/TITS.2023.3331885`; IEEE T-ITS 25(6), 5474–5487 (2024).
- Yin et al.: DOI `10.1109/TVT.2026.3660321`; IEEE TVT 75(7), 14681–14694 (2026).
- Memedi & Dressler: DOI `10.1109/COMST.2020.3034224`; IEEE COMST 23(1), 161–181 (2021).
- Gao et al.: DOI `10.1109/TNNLS.2021.3136866`; IEEE TNNLS 34(9), 6468–6479 (2023).
- Kumbul et al. waveform: DOI `10.1109/TAES.2022.3206173`.
- Kumbul et al. MIMO: DOI `10.1109/TMTT.2022.3228950`.
- Liu et al.: DOI `10.1109/LPT.2025.3649597`; IEEE Photonics Technology Letters 38(14), 1032–1035 (2026).
