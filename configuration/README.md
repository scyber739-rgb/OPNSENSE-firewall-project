# Configuration register

This register summarizes the lab configuration without publishing actual host IP addresses. Keep real address values in private lab notes only.

## Policy documentation format
| Rule ID | Interface/direction | Action | Protocol | Source | Destination | Port | Business justification | Verification |
|---|---|---|---|---|---|---|---|---|

## Alias register
| Alias purpose | Alias type | Members recorded | Usage | Verification |
|---|---|---|---|---|
| Kali test host | IP / host entry | KALI_HOST | Source of a TCP/80 PASS rule toward UBUNTU_SERVER | Alias and rule entered; curl test pending |

**Note:** Only one host address is currently recorded in this alias. It demonstrates a named host object; a multi-host group has not yet been populated or tested. Confirm the exact alias name from the firewall UI before recording it as a literal identifier.

## Day 3 HTTP test
| Component | Masked identifier | Purpose |
|---|---|---|
| Kali client | KALI_HOST | Sends the HTTP test request |
| Ubuntu server | UBUNTU_SERVER | Runs the Python HTTP server |
| Service | TCP/80 | HTTP test target |
| Firewall interface | OPT1 | Interface where Kali-originated traffic was evaluated |

## NAT documentation format
| NAT ID | External interface/address:port | Internal destination:port | Associated filter rule | Test client | Observed result |
|---|---|---|---|---|---|

## Change-control notes
For every change, record the original rule, the change, expected outcome, actual outcome, rollback action and evidence reference. Avoid publishing raw firewall configuration exports containing secrets or sensitive identifiers.
