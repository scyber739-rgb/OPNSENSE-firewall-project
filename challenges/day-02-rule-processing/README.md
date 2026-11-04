# Day 02 — Firewall dashboard, PASS/BLOCK rules and rule order

**Progress: Concepts and rule-order practice covered.** Preserve screenshots and test output as evidence when available.

## Business scenario
An organization needs to permit business traffic while blocking unwanted connections. Overlapping rules must be ordered correctly so that a broad allow rule does not override a more restrictive policy.

## Objectives
- Navigate Firewall → Rules and select the correct interface tab.
- Understand the rule editor fields.
- Create PASS and BLOCK rules.
- Understand source, destination, protocol and port matching.
- Observe how rule order changes the outcome.

## Rule editor — important fields
| Field | Purpose |
|---|---|
| Action | PASS allows matching traffic; BLOCK denies it |
| Interface | Network interface where the rule is evaluated |
| Address family | IPv4 or IPv6 |
| Protocol | TCP, UDP, ICMP or another supported protocol |
| Source | Originating host, network or alias |
| Destination | Target host, network or alias |
| Destination port | Service port on the target, when applicable |
| Log | Enables logging for matching traffic |
| Description | Human-readable reason for the rule |

## Hands-on procedure
1. Open Firewall → Rules.
2. Select the interface through which the test traffic enters.
3. Choose Add to create a rule.
4. Select the intended action: PASS for permitted traffic or BLOCK for denied traffic.
5. Select the address family and protocol appropriate to the test.
6. Set the source and destination as narrowly as possible.
7. Set a destination port only when the protocol/service requires it.
8. Add a meaningful description and enable logging for the test rule.
9. Save and apply the rule.
10. Review the rule list and confirm its order relative to other rules.

## Rule-order exercise
A specific BLOCK rule must be placed above a broader PASS rule when the intention is to deny that specific traffic. If a broader PASS rule matches first, the intended restrictive rule may never be reached.

| Test case | Intended policy | Evidence to collect |
|---|---|---|
| Traffic matching a specific BLOCK rule | Deny | Failed client test and matching BLOCK log |
| Traffic matching a specific PASS rule | Allow | Successful client test and matching PASS log |
| Traffic not allowed by any rule | Default deny | Deny log / firewall live view |

## Concepts learned
- Rules are evaluated in order on the relevant interface.
- Specific source/destination matching is safer than broad “any” matching.
- PASS and BLOCK are policy actions; they are not interchangeable.
- Logging helps identify which traffic matched a rule.
- A client-side timeout alone does not prove which rule caused the failure.

## Evidence checklist
- [ ] Dashboard Firewall → Rules screenshot
- [ ] PASS rule screenshot
- [ ] BLOCK rule screenshot
- [ ] Rule-order screenshot showing the specific rule above the broader rule
- [ ] Client test outputs and corresponding firewall logs

## Key lesson
A firewall policy is only effective when its action, interface, match criteria and order all align with the real packet path.
