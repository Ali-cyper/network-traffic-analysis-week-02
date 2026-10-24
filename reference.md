# Reference — Week 02

Quick reference built during the week. General Wireshark and protocol knowledge, not a record of any specific case.

## Reading a connection

| Observation | Typical meaning | Verify next |
| --- | --- | --- |
| SYN → SYN-ACK → ACK | Handshake completed | Application data and responses after the handshake |
| SYN → RST | Port closed or connection refused | Whether this repeats across many ports (scan behavior) |
| SYN → SYN-ACK, then no data | Port open, session may not have been used | Whether a client completes the handshake |
| SYN with no reply | Dropped or filtered, or host unreachable | Other traffic to the same host |

A completed handshake shows the connection was established. It does not show what the application did. Always read what follows.

## HTTP responses

| Code | Meaning |
| --- | --- |
| 200 OK | Request succeeded |
| 201 Created | A resource was created (typical for successful POST/upload) |
| 404 Not Found | Resource does not exist (the request failed, but the server was reachable) |

## Statistics → Conversations workflow

1. Open Statistics → Conversations.
2. Review each protocol tab (Ethernet, IPv4, TCP, UDP) for endpoints, packet counts, bytes, and duration.
3. Identify high-volume, long, or unusual flows, and note direction of data (bytes A→B vs B→A).
4. Select a conversation and apply it as a filter, then read the stream.

Single-frame length does not show how much data moved in a conversation.

## Display filter reference

| Goal | Filter |
| --- | --- |
| One host (either direction) | `ip.addr == 10.10.10.99` |
| One TCP stream | `tcp.stream eq 5` |
| Specific port | `tcp.port == 22` |
| Connection attempts (SYN, no ACK) | `tcp.flags.syn == 1 && tcp.flags.ack == 0` |
| Open-port responses (SYN-ACK) | `tcp.flags.syn == 1 && tcp.flags.ack == 1` |
| Resets (refused or closed) | `tcp.flags.reset == 1` |
| DNS for a name | `dns.qry.name == "example.com"` |
| HTTP requests | `http.request` |
| HTTP POST requests | `http.request.method == "POST"` |
| HTTP responses by code | `http.response.code == 200` |
| FTP login success | `ftp.response.code == 230` |
| ICMP | `icmp` |

Combine with `&&`, `||`, and `!` to isolate one conversation, then validate the stream before drawing a conclusion.

## Reference captures (post-hoc review)

Written afterward from capture files that remained in my library. This is **not** a record of conclusions I wrote during the original exercise. Addresses come from documentation ranges, so the material is simulated.

- **`training_level1.pcap` (14 packets):** ICMP to the gateway, a DNS query for `example.com`, then a completed TCP session to port 80 with `GET /` answered by `HTTP/1.1 200 OK`. The request succeeded.
- **`soc_beginner_20_events.pcap` (105 packets, about 37 s):** multiple unrelated activities in one file: routine DNS and HTTP, repeated failed SSH authentication for `admin`, a targeted scan of ports 22/80/443/445/3389 with mixed `RST` and `SYN-ACK` replies, a successful FTP login, an HTTP `/beacon` request followed by a separate `POST /upload` returning `201`, and `404` / `ACCESS_DENIED` responses. Lesson: describe what each response proves, and do not treat activities in one file as one incident by default.
