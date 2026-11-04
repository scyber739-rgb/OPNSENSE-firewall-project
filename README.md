# OPNsense Enterprise Firewall Engineering Lab

**15-day practical network security and firewall engineering project** | VirtualBox · OPNsense · Kali Linux · Ubuntu · Windows

## Project overview
I am building a controlled virtual enterprise network to understand how firewalls enforce security boundaries. Rather than collecting configuration screenshots alone, I am documenting why each rule exists, the packet path it affects, how I tested it, what failed, and what the evidence actually shows.

**Status:** Days 1–2 concepts and experiments covered; Day 3 remains in progress; Day 4 alias configuration and a TCP/80 pass rule have been entered, but traffic verification is pending. The Windows → OPNsense → internal LAN topology is **proposed, not yet deployed or validated**.

## Objectives
- Build a reproducible virtual network with distinct outside and inside trust zones.
- Configure and validate inbound and outbound rules, state tracking, NAT, aliases, and segmentation.
- Explore IDS/IPS, VPN, monitoring, backup, and incident response.
- Produce traceable evidence: command outputs, packet captures, rule screenshots, timestamps, and observed outcomes.
- Record failed tests without presenting them as successful deployments.

## Proposed architecture
```text
Physical Windows host (outside test client)
              |
    OPNsense outside-facing interface
        [routing / firewall / NAT]
    OPNsense inside-facing interface
              |
        Internal virtual LAN
           /       \
     Kali Linux   Ubuntu HTTP server
```
Kali and Ubuntu on the same Layer-2 LAN can communicate directly without crossing OPNsense; their east-west traffic is **not** protected by OPNsense merely because the firewall is their gateway. Windows-to-internal traffic must be deliberately routed/forwarded through OPNsense without a bypass path. VirtualBox adapter selection and addressing will be validated in the later topology challenge. All IPs shown in this repository are lab examples or redacted.

## Progress
| Day | Focus | Evidence status |
|---|---|---|
| 01 | Basic firewall policy and logging | Concepts/lab covered; screenshots pending |
| 02 | Rule matching, order and conflicts | Concepts/lab covered; screenshots pending |
| 03 | Internal web access and stateful inspection | In progress; timeout/block observations recorded |
| 04 | IP aliases and alias-based firewall policy | Alias with one host IP and TCP/80 pass rule configured; curl verification pending |
| 05–15 | Remaining advanced topics | Planned |

See [the complete roadmap](ROADMAP.md) and [daily challenge notes](challenges/).

## Repository navigation
- [Architecture](architecture/README.md) — proposed topology, IP planning and packet paths
- [Configuration](configuration/README.md) — policies, aliases, NAT and change control
- [Challenges](challenges/README.md) — day-by-day work
- [Troubleshooting](troubleshooting/incident-journal.md) — observed problems and investigation
- [Evidence](evidence/README.md) — screenshots and capture requirements
- [Final report](final-report/README.md) — capstone assessment template
- [LinkedIn posts](linkedin-posts/README.md) — evidence-backed communication

## Validation standard
Each day distinguishes **planned**, **configured**, **observed**, and **verified**. A timeout is not proof of a particular firewall rule; a logged ICMP block is not evidence that HTTP was blocked. Screenshots and tests will be added after they are actually collected.

## Safety
This is an authorized isolated homelab. Do not expose test servers to public networks. Remove or redact real credentials, public IPs, host identifiers and sensitive network details before publishing.

## Next milestone
**Day 4 verification:** test Kali → Ubuntu HTTP access through the alias-based rule, inspect the matching firewall log/state, then test a controlled block. Only after collecting the output will the result be marked verified.
