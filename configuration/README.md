# Configuration register

Configuration snapshots and screenshots will be added only after deployment and validation.

## Policy documentation format
| Rule ID | Interface/direction | Action | Protocol | Source | Destination | Port | Business justification | Verification |
|---|---|---|---|---|---|---|---|---|

## NAT documentation format
| NAT ID | External interface/address:port | Internal destination:port | Associated filter rule | Test client | Observed result |
|---|---|---|---|---|---|

## Change-control notes
Record the original rule, the change, expected outcome, actual outcome, rollback action and evidence reference. Avoid publishing raw firewall configuration exports containing secrets or sensitive identifiers.
