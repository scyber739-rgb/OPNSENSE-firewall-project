# Architecture and traffic-flow plan

## Target design (not yet deployed)
Windows physical host acts as an outside test client. OPNsense separates the outside-facing test network from an internal VirtualBox LAN containing Kali and Ubuntu.

```text
Windows (outside) -- OPNsense WAN | firewall / NAT | OPNsense LAN -- internal switch -- Kali + Ubuntu
```

### Design decisions
- Use separate virtual networks for outside and inside; do not attach Windows directly to the internal LAN for the inbound firewall demonstration.
- Kali and Ubuntu share one Layer-2 LAN. Direct Kali↔Ubuntu traffic does not necessarily traverse OPNsense.
- Select an outside-facing VirtualBox adapter mode that lets the physical Windows host reach OPNsense while keeping lab services isolated.
- Verify gateway, subnet, routes, listening sockets, return path and policy before claiming any inbound NAT success.
- Port forwarding alone is insufficient unless the associated filtering policy permits the intended traffic.
- Do not treat OPNsense's own successful HTTP request as proof of Windows→LAN reachability.

## Address inventory
Historical lab observations (not a confirmed current topology): Kali `192.168.254.3`, Ubuntu `192.168.1.2`; gateway/interface assignments changed during earlier experiments. Current addressing is **TBD** and must be measured again after redesign.

## Required evidence
VirtualBox adapter screenshots, OPNsense interface assignments, Windows routes, Kali/Ubuntu routes, firewall/NAT rules, and two-sided packet captures.
