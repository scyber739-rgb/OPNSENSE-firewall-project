# OPNsense Enterprise Firewall Engineering Lab

**15-day practical network security and firewall engineering project** | VirtualBox · OPNsense · Kali Linux · Ubuntu · Windows

## Project overview
This project documents the design, configuration and validation of a controlled virtual firewall lab. Each daily challenge records the business scenario, security objective, configuration steps, traffic path, test method, expected and actual results, troubleshooting notes, and evidence still required.

**Current progress:** Day 1 interface and initial policy practice; Day 2 PASS/BLOCK rules and rule ordering; Day 3 protocol/port filtering using an Ubuntu Python HTTP server and Kali curl tests; Day 4 IP alias creation and an alias-based TCP/80 PASS rule. Day 4 traffic verification is still pending.

## Lab components
- OPNsense firewall dashboard
- Kali Linux — authorized test client
- Ubuntu Linux — HTTP test server
- VirtualBox — isolated virtual networking
- Windows host — potential external test client in a later topology exercise

## Proposed traffic model
    Test client (Kali / Windows)
              |
       OPNsense firewall
       [policy / routing]
              |
       Internal lab server
          (Ubuntu HTTP)

The actual packet path must be confirmed for each test. Traffic between two VMs on the same Layer-2 network can bypass the firewall, even if OPNsense is configured as their default gateway. Do not assume a rule is filtering traffic unless the route and ingress interface prove that packets traverse the firewall.

## Day-by-day progress
| Day | Topic | Work recorded | Current status |
|---|---|---|---|
| 01 | Interface setup and firewall fundamentals | Dashboard, WAN/LAN/OPT1 roles, initial policy workflow | Covered; evidence screenshots pending |
| 02 | PASS/BLOCK rules and rule order | Rule editor fields, source/destination matching, specific vs broad rules | Covered; evidence screenshots pending |
| 03 | Protocol and port filtering | Ubuntu Python HTTP server, Kali curl baseline, TCP/80 BLOCK rule | Practiced; attach terminal and log evidence |
| 04 | IP aliases | IP alias created with Kali host; alias used as source in TCP/80 PASS rule | Configured; curl/log verification pending |
| 05–15 | Advanced firewall engineering | Segmentation, NAT, DHCP/DNS, monitoring, VPN, HA, IDS/IPS and capstone | Planned |

## Repository navigation
- [15-day roadmap](ROADMAP.md)
- [Daily challenge index](challenges/README.md)
- [Day 01 — Firewall setup](challenges/day-01-firewall-basics/README.md)
- [Day 02 — PASS/BLOCK and rule order](challenges/day-02-rule-processing/README.md)
- [Day 03 — Protocol and port filtering](challenges/day-03-stateful-inspection/README.md)
- [Day 04 — IP aliases](challenges/day-04-aliases/README.md)
- [Configuration register](configuration/README.md)

## Evidence and accuracy standard
A configured rule is not automatically a verified result. Each test must include the actual client command/output and a corresponding firewall log where possible. A timeout alone does not prove a firewall block. Screenshots and logs should be added only after they are captured from the lab.

## Address masking and safety
Public documentation uses role labels such as **KALI_HOST** and **UBUNTU_SERVER** instead of actual IP addresses. Keep the real values only in the private lab notes. Never publish credentials, sensitive host details, or unredacted firewall exports. Keep test services isolated and do not expose them to the public internet.

## Next action
Finish Day 4 by testing HTTP access through the alias-based PASS rule, collecting the curl output and matching firewall log, then performing a controlled BLOCK test if the PASS baseline is confirmed.
