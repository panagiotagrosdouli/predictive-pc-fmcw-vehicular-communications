# Link-Model Audit — Paper 1

The local `LinkModel` is a geometry-dependent, reference-SNR-anchored abstraction. It applies geometric beam spreading, optional atmospheric attenuation, a pointing term, field-of-view gating, BER mapping, packet-error mapping, and goodput/outage rules. The code preserves the repository's monotonicity validation but is not an absolute measured optical link budget.

`received_power_calibrated` is false in the reference configuration. The Part-A provenance also states that the supplied upstream notebook was not locally rerun and that no measured optical channel is claimed. The code docstring has therefore been changed from “calibrated” to “reference-SNR-anchored” without changing numerical behavior.

PER is computed from BER under an independent-bit-error packet abstraction, `1-(1-BER)^packet_bits`. This is a model assumption and must not be represented as a measured packet-error curve. Paper 1 may discuss packet-level simulator outcomes under this abstraction; it may not imply hardware packet measurements.
