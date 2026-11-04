# Day 04 — IP aliases and alias-based firewall policies

**Status: CONFIGURED — traffic verification pending.** This record reflects the lab work described in the session. It does not claim that the HTTP test succeeded.

## Business scenario
A small organization has multiple endpoints that need the same access policy. Maintaining a separate firewall rule for every endpoint becomes difficult. An IP alias groups one or more host addresses under a reusable name, allowing a rule to reference the group.

## Security objective
Create an IP alias, use it as a firewall rule source, and validate that the rule applies to the intended endpoint(s). Keep the rule narrowly scoped to the required destination and service.

## Lab context
- Firewall platform: OPNsense lab (the session sometimes refers to pfSense generically).
- Kali test host: `192.168.20.10`.
- Ubuntu HTTP server: `192.168.1.2`.
- HTTP service: TCP port `80`.
- Interface context: Kali traffic enters through the OPT1-side lab network.

All addresses are lab-only examples. Mask or replace them before publishing screenshots if they reveal sensitive topology details.

## Configuration recorded
1. Opened **Firewall → Aliases → IP** and created an IP alias.
2. Added the Kali host address `192.168.20.10` as a member and saved the alias.
3. Configured a firewall rule using the alias as the source, Ubuntu `192.168.1.2` as the destination, TCP as the protocol, destination port `80`, and **Pass** as the action.
4. The exact alias display name and rule identifier were not captured in the transcript; confirm them from the firewall UI before adding screenshots or quoting those identifiers.

### Important scope clarification
Only one IP address (`192.168.20.10`) was added during this exercise. The alias demonstrates referencing a host through a reusable name, but a multi-host group has **not** yet been populated or tested. Additional host IPs can be added as separate entries in the same alias if they should receive the same policy.

## Intended packet path
```text
Kali (192.168.20.10)
        |
        | TCP destination port 80
        v
OPNsense OPT1 firewall rule
  Source: created IP alias
  Destination: Ubuntu (192.168.1.2)
  Action: Pass
        |
        v
Ubuntu HTTP server (TCP/80)
```

The firewall rule only governs traffic that actually traverses the firewall on the interface where the rule is applied. Confirm the interface and routing path before interpreting test results.

## Validation plan — NOT YET VERIFIED
From Kali, run:

```bash
curl -v --connect-timeout 5 http://192.168.1.2/
```

Expected if the path, server, and rule are all correct: an HTTP response from Ubuntu. Record the actual curl output and timestamp.

Then:
- [ ] Confirm the corresponding TCP/80 pass entry in the firewall live log.
- [ ] Confirm the connection/state entry while the session is active, if available.
- [ ] Add a temporary, narrowly scoped block test only after capturing the pass baseline.
- [ ] Verify the block using both curl output and a matching firewall log entry.
- [ ] Remove or disable the temporary test block and confirm the intended pass policy again.

A curl timeout alone does not prove that the alias rule blocked the traffic. Check routing, interface selection, server listening state, host firewall and firewall logs.

## Expected vs actual
| Item | Expected | Actual status |
|---|---|---|
| IP alias | Contains Kali host address | Created and saved, according to session |
| Alias as rule source | Rule references the alias | Configured, according to session |
| TCP/80 pass rule | Kali alias → Ubuntu host | Entered; screenshot/rule ID pending |
| HTTP request | Ubuntu returns HTTP response | Not yet tested / output not supplied |
| Firewall log | Matching TCP/80 pass event | Not yet captured |
| Multi-host alias | Multiple host addresses share one rule | Not done; only one address added |

## Evidence checklist
- [ ] Alias details screenshot (name and address visible; sensitive details masked)
- [ ] Firewall rule screenshot (interface, action, protocol, source alias, destination and port)
- [ ] Kali curl output with timestamp
- [ ] Matching firewall log entry
- [ ] Optional block-test output and corresponding deny log

## Lesson
An alias is a reusable address object, not a firewall rule by itself. The rule defines the action; the alias supplies one or more source or destination addresses. A one-host alias can be useful, and the same alias can later contain multiple hosts.

## Next step
Complete the HTTP pass test and collect log evidence. After that, test a controlled block and then add another host address to demonstrate that one rule can cover multiple systems.
