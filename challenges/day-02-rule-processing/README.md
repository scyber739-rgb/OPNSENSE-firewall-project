# Day 02 — Rule order and policy matching

**Status: Concepts and lab experiments covered; evidence pending.**

## Business scenario
Overlapping allow/deny policies can cause unexpected access or outages. An engineer must predict the matching rule and prove it using traffic tests.

## Security objective
Understand source/destination matching, interface direction, specific vs broad policies and rule priority.

## Work recorded from prior lab sessions
- Explored specific vs broad rules and PASS/BLOCK conflicts.
- Tested the effect of placing an ICMP block above a broader PASS rule.
- Discussed default deny and how incoming interface selection changes which rules apply.

## Decision matrix to validate
| Test | Intended policy | Proof required |
|---|---|---|
| Matching ICMP source/destination | Block | Logged deny + failed ping |
| Allowed TCP destination | Pass | Successful request + matching policy/state |
| Source not covered by allow rule | Default deny | Logged deny and rule trace |

These are **test intentions**, not verified results for this repository.

## Evidence to add
- [ ] Rule list before and after reorder
- [ ] Actual source/destination and test commands
- [ ] PASS/BLOCK logs with timestamps
- [ ] Written explanation of the first matching rule

## Lesson
A correct-looking rule can be ineffective if traffic enters on another interface, an earlier rule matches, or traffic bypasses the firewall.
