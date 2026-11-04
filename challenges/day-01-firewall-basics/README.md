# Day 01 — Firewall setup, interfaces and first policy

**Progress: Covered in the lab.** Screenshots and exact command outputs should be attached from the actual environment before claiming independent evidence verification.

## Business scenario
A small company needs to place a firewall between its network zones. Before writing security rules, the engineer must understand the interfaces, IP addressing and traffic path.

## Objectives
- Access and navigate the firewall web dashboard.
- Identify WAN, LAN and OPT1 interfaces and understand their roles.
- Check a client machine's IP address, subnet mask, default gateway and routes.
- Understand which interface receives a packet and where its rule is evaluated.
- Create and inspect an initial firewall rule.

## Hands-on workflow
1. Open the firewall dashboard from a permitted management client.
2. Review the interface overview and identify WAN, LAN and OPT1.
3. Check the client network settings using the operating system's IP configuration and route commands.
4. Match each VirtualBox network adapter to the intended firewall interface and lab network.
5. Open Firewall → Rules and select the interface through which the test traffic enters.
6. Inspect the default rules before adding anything.
7. Create a narrowly scoped test policy, save it and apply the changes.
8. Review the rule list and firewall live log.

## Concepts learned
- WAN is the outside-facing interface; LAN is the internal network; OPT1 is an additional interface/zone.
- A firewall rule is associated with an interface and direction. A rule on one interface does not automatically filter traffic entering another.
- Source identifies where the packet originates; destination identifies where it is going.
- PASS permits matching traffic; BLOCK denies matching traffic.
- The firewall dashboard is used to configure policies and inspect their status/logs.

## Validation and evidence
The lab work covered dashboard navigation, interface identification and initial rule configuration. Keep these evidence items with the repository:
- [ ] Dashboard interface overview (mask addresses and host identifiers)
- [ ] Client IP configuration and route output (redacted)
- [ ] First rule screenshot showing interface, action, protocol, source and destination
- [ ] Matching live-log entry with timestamp

## Result discipline
Do not invent an exact rule ID, IP address, timestamp or successful test output if it was not saved. Add screenshots only after capturing them from the lab.

## Key lesson
Understand the packet path and ingress interface before creating a rule. A correctly written rule on the wrong interface will not control the traffic you intend to filter.
