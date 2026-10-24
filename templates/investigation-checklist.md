# PCAP Investigation Checklist

Complete before writing any verdict.

## Inventory
- [ ] Packet count, time span, protocols recorded
- [ ] All hosts and targets listed and counted

## Triage
- [ ] Statistics → Conversations reviewed (not single frames)
- [ ] Source, destination, port, protocol, and direction noted per important conversation

## Verification
- [ ] Events sorted by actual timestamp, not row order
- [ ] TCP handshake outcome stated for each classified connection
- [ ] Actual application response read (for example HTTP status code)

## Correlation
- [ ] Two activities linked only by same IP and stream, or independent evidence
- [ ] Time gap, destination, and data volume compared

## Before the verdict
- [ ] Written in order: observation, hypothesis, missing evidence
- [ ] Second incident checked for
- [ ] Benign or misleading activity checked for
- [ ] Classification supported by evidence, not only by resemblance
