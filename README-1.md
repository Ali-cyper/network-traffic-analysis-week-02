# Week 02 — Network Traffic Analysis (PCAP / Wireshark)

[العربية](README.AR.md)

Part of my SOC Investigation Curriculum · Previous: [Week 01 — Windows Event Logs](https://github.com/Ali-cyper/windows-event-log-investigation-week-01)

## Summary

Week 2 moves from host evidence (Windows event logs) to network evidence. I investigated packet captures in Wireshark with one goal: build a hypothesis from full conversations and verified details, not from the overall shape of the traffic.

PCAP analysis was my weakest area going in. I understood protocols in theory but did not know where to start with an open capture and needed hints to form a first hypothesis.

## Repository structure

```
week-02/
├── README.md            Week summary, results, top mistakes
├── cases/               Case reports in my own words (as submitted) + post-review corrections
├── mistake-log.md       Every mistake, root cause, and the rule it produced
├── reference.md         Protocol, handshake, response-code, and Wireshark filter reference
└── templates/
    ├── case-report-template.md
    └── investigation-checklist.md
```

## Scope and materials

- Five incident-investigation PCAPs of escalating difficulty
- Capture data is **synthetic** and was generated for training; case review was AI-assisted **after** my own attempt
- Tools: Wireshark (Statistics → Conversations, display filters)

## Method

Each case followed the [investigation checklist](templates/investigation-checklist.md): inventory the capture, triage with Conversations, verify each connection's outcome, order events by timestamp, separate observation from hypothesis, link activities only with evidence, and check for a second incident before the verdict.

## Results

| Area | Start of week | End of week |
| --- | --- | --- |
| Reading a capture | Frame-by-frame, no clear starting point | Conversation-level triage with Statistics → Conversations |
| Evidence handling | Verdict reached from the first plausible story | Searched for a second incident without prompting |
| Correlation | Linked events by similarity or closeness | Separated two incidents using path, host, and data volume |
| Confidence | Stated conclusions as facts | Stated "likely, but not sufficient alone" and asked for more evidence |
| Display filters | Self-identified weakness | Still open |

## Top mistakes

1. **Classified by general shape before verifying details.** A port scan was labeled DDoS, and later a fully successful connection was labeled "rejected." The same root cause appeared twice.
2. **Stopped at the first convincing explanation** while a second activity was present in the capture.
3. **Assumed row order equals time order** and merged a login with a file transfer that were far apart in time.

Full list with root causes and rules: [mistake-log.md](mistake-log.md)

## Open items

- Wireshark display filters need more hands-on practice; I have no recorded evidence yet of fully independent use.
- Before writing a verdict I must state the handshake outcome and the application response for every connection I classify.

## Accuracy note

This repository was reconstructed from saved assessment notes and the capture files that remained. The original conversations and every case answer were not fully recoverable, so nothing here is a verbatim record, and no details were invented to fill gaps. Material described as post-hoc review is labeled as such.
