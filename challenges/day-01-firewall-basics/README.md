# Day 01 — Firewall fundamentals and basic policies

**Status: Concepts and lab experiments covered; independent screenshot verification pending.**

## Business scenario
A small organization needs a perimeter firewall that can permit necessary traffic and deny unwanted access while producing auditable logs.

## Security objective
Learn interface-based policy enforcement, basic PASS/BLOCK rules, ICMP testing, and firewall live logs.

## Work recorded from prior lab sessions
- Practiced creating basic firewall PASS/BLOCK policies.
- Practiced an ICMP block above a broader pass and checked ping behavior and logs.
- Used client-side tests including `ping` and `curl` to reason about rule effects.

## Expected vs actual
**Expected:** matching blocked traffic should be denied and, with logging enabled, appear in the firewall logs.
**Reported observation:** earlier practice included blocked ping behavior and log inspection. Exact command output, timestamps, rule identifiers, and screenshots have not been retained here; the result is **not independently verified**.

## Evidence to add
- [ ] Interface/rule screenshot with identifying information masked
- [ ] Before-and-after ping output
- [ ] Corresponding live log entry and timestamp
- [ ] Rule ordering screenshot

## Lesson
Policy order, interface direction and observability matter. A client timeout by itself does not identify which rule caused it.
