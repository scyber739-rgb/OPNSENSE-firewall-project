# Day 04 — IP aliases and reusable firewall policies

**Progress: Alias created and referenced by a TCP/80 PASS rule. Traffic verification is pending.**

## Business scenario
A company has several systems that require the same network policy. Creating and maintaining a separate rule for every host increases administrative effort and the chance of inconsistent changes. An IP alias groups host addresses under one reusable object, which can then be referenced by firewall rules.

## Security objective
Create an IP alias, use it as a rule source, and validate that the rule applies only to the intended destination and service.

## Lab roles
- Kali Linux: test client, documented as **KALI_HOST**.
- Ubuntu Linux: HTTP destination, documented as **UBUNTU_SERVER**.
- Firewall: OPNsense lab dashboard.
- Test service: HTTP over TCP destination port **80**.

Actual IP addresses are intentionally masked in this public repository. Use the live lab configuration to substitute the real values during testing.

## What is an alias?
An alias is a named group/object containing one or more IP addresses, networks, ports or URLs (depending on alias type). Instead of repeatedly entering individual addresses in multiple rules, an administrator can refer to the alias by name.

Example: an alias named **HR_HOSTS** could contain all approved HR workstation IP addresses. A single rule can then reference HR_HOSTS as its source. If a workstation is added or replaced, update the alias membership rather than recreating every rule that uses it.

An alias does not itself allow or block traffic. The firewall rule defines the action; the alias supplies the match criteria.

## Configuration recorded
1. Opened **Firewall → Aliases → IP**.
2. Created an IP/host alias and entered the Kali test host address. The exact alias name shown in the UI was not captured; confirm it in the firewall before documenting a literal name.
3. Saved the alias.
4. Opened the relevant firewall rule editor.
5. Selected the created alias as the **Source**.
6. Set the destination to the Ubuntu HTTP server, protocol to **TCP**, destination port to **80**, and action to **Pass**.
7. Saved the rule.

Only **one host address** was added in this session. This demonstrates alias use, but a multi-host alias has not yet been populated or tested.

## Intended policy
| Setting | Value |
|---|---|
| Interface | OPT1 (confirm against actual traffic path) |
| Action | PASS |
| Address family | IPv4 |
| Protocol | TCP |
| Source | Created Kali host alias (KALI_HOST) |
| Destination | Ubuntu HTTP server (UBUNTU_SERVER) |
| Destination port | HTTP / TCP 80 |
| Logging | Enable for validation |
| Description | Allow aliased Kali test host to Ubuntu HTTP |

## Traffic path
    KALI_HOST  →  Firewall OPT1 rule  →  UBUNTU_SERVER:TCP/80

The rule only filters traffic that actually traverses the firewall on the interface where it is applied. If two VMs share the same Layer-2 network, their direct traffic may bypass the firewall.

## Validation plan — pending
From Kali, run:

    curl -v --connect-timeout 5 http://UBUNTU_SERVER:80/

Replace UBUNTU_SERVER locally with the actual Ubuntu lab address. If the rule and network path are correct and the Python HTTP service is running, the request should receive an HTTP response.

Then:
- [ ] Capture the actual curl output and timestamp.
- [ ] Confirm a matching TCP/80 PASS entry in the firewall live log.
- [ ] Confirm the active connection/state if available.
- [ ] Add a second lab host to the same alias only if one is available and intended to receive the same policy.
- [ ] Verify that the same rule matches the second host.
- [ ] Optionally perform a controlled BLOCK test after capturing the PASS baseline.

A timeout alone does not prove the alias rule blocked traffic. Check routing, ingress interface, server listener, host firewall and matching firewall log.

## Expected vs actual
| Item | Expected | Current record |
|---|---|---|
| IP alias | Named host object exists | Created and saved |
| Alias membership | Contains the Kali test host | One host address added |
| Firewall rule | Alias → Ubuntu server, TCP/80, PASS | Entered in rule editor |
| HTTP test | Ubuntu returns an HTTP response | Not yet reported |
| Firewall log | Matching TCP/80 PASS event | Not yet captured |
| Multiple hosts | One alias contains multiple host addresses | Not yet done |

## Evidence checklist
- [ ] Alias configuration screenshot with address values masked
- [ ] OPT1 rule screenshot showing alias source and TCP/80 destination
- [ ] Kali curl output
- [ ] Matching firewall live-log entry
- [ ] Optional second-host test evidence

## Key lesson
Aliases make firewall policies easier to maintain. One alias can contain multiple hosts, and one rule can reference that alias. The alias is the reusable address group; the firewall rule still determines PASS or BLOCK.

## Next action
Complete the HTTP PASS test and collect its log evidence. Then test a controlled BLOCK policy and, if a second host is available, add it to the alias to demonstrate multi-host grouping.
