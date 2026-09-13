# Packet Deadline Semantics

The simulator is slotted. A packet arriving at the start of slot `a` with an exactly representable physical deadline spanning `N` slots may be served in slots `a, ..., a+N-1`. Its inclusive last-service index is therefore `a+N-1`; at the start of slot `a+N` it is expired.

Physical deadlines supplied in seconds must be an integer multiple of `slot_duration_s`. The simulator fails closed for sub-slot or non-integral deadlines instead of silently rounding them. This is required because deadline values are scientific experimental factors rather than UI conveniences.

With the Paper-1 reference slot duration of 0.1 s, the tightest representable positive deadline is 0.1 s. The historical 0.05 s regime is retained only as pre-correction provenance and is replaced by a frozen 0.1 s regime for corrected revalidation.
