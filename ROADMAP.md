# 15-Day Firewall Engineering Roadmap

Each challenge includes: business scenario, security objective, network path, prerequisites, configuration, validation, expected vs actual results, logging evidence, troubleshooting, and reflection. A day is complete only when the relevant tests have been verified.

| Day | Challenge | Deliverable |
|---|---|---|
| 01 | Firewall fundamentals: interfaces, PASS/BLOCK, logs | Basic policy evidence |
| 02 | Rule order, source/destination matching, conflicting policies | Rule decision matrix |
| 03 | Protocol/port rules and stateful inspection (ICMP, HTTP, SSH) | Protocol-specific test results |
| 04 | IP aliases and alias-based firewall policies | Reusable host groups and verified policy tests |
| 05 | Network segmentation and VLANs | Segmentation validation matrix |
| 06 | Outbound NAT and address translation | NAT packet-path comparison |
| 07 | Port forwarding and inbound access control | Controlled external-to-internal service test |
| 08 | DHCP and DNS security | Addressing and name-resolution policy tests |
| 09 | Firewall logs and monitoring | Evidence-backed event investigation |
| 10 | VPN (OpenVPN/IPsec) | Secure remote-access validation |
| 11 | High availability (CARP) and failover | Primary/backup failover test |
| 12 | IDS/IPS with Suricata | Controlled detection and prevention evidence |
| 13 | Advanced policies, floating rules and schedules | Policy review and test matrix |
| 14 | Troubleshooting and security auditing | Regression and troubleshooting report |
| 15 | Enterprise firewall deployment capstone | Final architecture, audit and interview defense |

**Scope note:** Some advanced labs may require additional virtual adapters, VLAN-capable topology or resources. Plan changes and skipped items must be documented explicitly rather than claimed complete.
