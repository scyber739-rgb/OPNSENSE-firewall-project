# Day 03 — Internal server protection and stateful inspection

**Status: IN PROGRESS — HTTP success and state-table behavior not yet verified.**

## Business scenario
An internal Ubuntu HTTP server must be reachable only through an intended security boundary. ICMP and TCP access should be governed by explicit policies.

## Historical lab context
Earlier experiments used Kali `192.168.254.3` and Ubuntu `192.168.1.2` on different subnets, with Kali-side traffic reported on OPNsense OPT1. This was an earlier topology and is not the proposed same-LAN redesign.

## Recorded tests and observations
1. A Python HTTP server was started on Ubuntu using port **80**, as clarified during the lab discussion. The exact launch command/output was not preserved.
2. From Kali, `curl -v --connect-timeout 5 http://192.168.1.2:80/` produced:
   ```text
   Trying 192.168.1.2:80...
   Connection timed out after 5003 milliseconds
   curl: (28) Connection timed out after 5003 milliseconds
   ```
3. The supplied OPNsense Live View showed **OPT1 / In / ICMP / 192.168.254.3 → 192.168.1.2 / block / Default deny / state violation rule**, repeated across several seconds. It also showed a blocked DHCP broadcast `0.0.0.0:68 → 255.255.255.255:67`.
4. These ICMP log entries **do not prove** the TCP/80 curl was blocked by that same rule. No matching TCP/80 deny entry was supplied.
5. We discussed stateful connection tracking: permitted flows can create states that allow legitimate return packets; a stateful firewall does not guarantee that application payloads are safe.

## Expected vs actual
| Test | Expected | Actual evidence | Assessment |
|---|---|---|---|
| Ubuntu HTTP listener | TCP/80 listening | Server reported running; socket output unavailable | Unverified |
| Kali → Ubuntu HTTP | Reachability before restrictive rule | curl timeout | Failed / cause unknown |
| Kali → Ubuntu ICMP | Subject to OPT1 policy | Default deny/state violation log entries | Observed block |
| TCP connection state | Visible when a connection is established | No successful session captured | Not tested successfully |

## Troubleshooting notes
Potential causes for the HTTP timeout include interface rules, routing/return path, host firewall and adapter connectivity. None is confirmed. The earlier troubleshooting is intentionally paused while the lab topology is redesigned.

## Day 03 completion criteria
- [ ] Establish a successful HTTP baseline in the validated topology
- [ ] Apply a targeted rule and confirm corresponding TCP/80 logs
- [ ] Observe an active state using a long-lived connection
- [ ] Compare new connections with established states
- [ ] Attach redacted screenshots and exact test outputs

## Lesson
Separate **what was observed** from **what is inferred**. A logged ICMP deny cannot be presented as proof of an HTTP deny.
