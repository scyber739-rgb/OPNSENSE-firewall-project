# Configuration register

Configuration snapshots and screenshots will be added only after deployment and validation.

## Policy documentation format
| Rule ID | Interface/direction | Action | Protocol | Source | Destination | Port | Business justification | Verification |
|---|---|---|---|---|---|---|---|---|

## Alias register
| Alias purpose | Alias type | Members recorded | Usage | Verification |
|---|---|---|---|---|
| Kali test host | IP / host entry | 192.168.20.10 | Source of a TCP/80 pass rule toward Ubuntu | Alias and rule entered; curl test pending |

**Note:** Only one host address is currently recorded in this alias. It is not yet a multi-host group. Confirm the exact alias name from the firewall UI before documenting it as a literal identifier.

## NAT documentation format
| NAT ID | External interface/address:port | Internal destination:port | Associated filter rule | Test client | Observed result |
|---|---|---|---|---|---|

## Change-control notes
Record the original rule, the change, expected outcome, actual outcome, rollback action and evidence reference. Avoid publishing raw firewall configuration exports containing secrets or sensitive identifiers.
