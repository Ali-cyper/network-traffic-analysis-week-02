# Mistake Log — Week 02

Each entry records what happened, why it was wrong, and the rule it produced. Status reflects the saved end-of-week assessment.

| ID | Mistake | Why it was wrong | Rule going forward | Status |
| --- | --- | --- | --- | --- |
| M-01 | Labeled a port scan as DDoS | A scan probes ports and services to learn what is exposed. DDoS floods a target to exhaust resources. Many connections alone do not distinguish them. | Describe what the traffic did (targets, ports, responses, volume) before naming an attack type. | Recurred as M-06 |
| M-02 | Missed one item when listing scan targets | An incomplete evidence inventory produces an incomplete conclusion. | Count targets with a checklist and verify the total. | Fixed |
| M-03 | Stopped at the first convincing explanation | The capture contained a second activity that the first story did not cover. | Always check for a second incident and for benign or misleading activity before the verdict. | Improved: searched unprompted in the final capture |
| M-04 | Merged a login and a file transfer that were far apart in time | Two activities in one file are not automatically one session or one incident. | Link events only through the same IP and stream, or independent evidence; check the time gap. | Fixed |
| M-05 | Assumed table row order equals chronological order | Row order is not guaranteed to match time. | Sort by the actual timestamp. | Fixed |
| M-06 | Described a fully successful connection as "rejected" | The classification came from overall shape, not from the handshake and the application response. Same root cause as M-01. | State the handshake outcome (SYN / SYN-ACK / ACK) and the actual response code before classifying. | Open |
| W-01 | Display-filter writing | Self-identified weakness. Slow manual scrolling instead of isolating a conversation. | Practice isolating by IP, port, protocol, and stream; see [reference.md](reference.md). | Open (no recorded evidence of independent use) |

## Pattern

M-01 and M-06 are the same mistake in two forms: **classifying from the overall shape of the traffic before verifying details.** The corrective step is a fixed pre-verdict check:

1. Did the TCP handshake complete?
2. What did the application actually return?
3. Does the evidence support this classification, or only resemble it?
