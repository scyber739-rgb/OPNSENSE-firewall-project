# Day 03 — Protocol and port filtering with an Ubuntu Python HTTP server

**Progress: HTTP baseline and HTTP blocking were practiced.** Exact screenshots, timestamps and complete terminal output should be added from the lab before independent evidence verification.

## Business scenario
An internal Ubuntu machine hosts a simple HTTP service. The security engineer must allow or block access to that service from a Kali test machine using a specific firewall rule, rather than blocking all traffic.

## Lab roles
- Kali Linux: authorized test client; address represented as **KALI_IP**.
- Ubuntu Linux: HTTP server; address represented as **UBUNTU_IP**.
- OPNsense: routes/filters traffic between the lab networks; the relevant incoming interface is OPT1.
- Service under test: HTTP over TCP destination port **80**.

All host addresses are intentionally masked in this public documentation.

## Objective
- Start a Python HTTP server on Ubuntu.
- Confirm the service is reachable from Kali before applying the restrictive rule.
- Create a specific TCP/80 BLOCK rule on the interface where Kali traffic enters.
- Test the result from Kali using curl.
- Understand why protocol and destination port are important match conditions.

## Step 1 — Start the HTTP server on Ubuntu
Run this in the Ubuntu terminal:

    sudo python3 -m http.server 80

Keep the terminal open while testing. The Python server serves files from the current working directory. Use a dedicated test directory with non-sensitive sample files; do not expose personal files.

## Step 2 — Baseline test from Kali
From Kali, request the Ubuntu server:

    curl -v --connect-timeout 5 http://UBUNTU_IP:80/

Replace UBUNTU_IP locally with the actual Ubuntu lab address. The initial lab test returned the Ubuntu Python server's directory listing, confirming HTTP reachability before the restrictive rule was applied.

## Step 3 — Configure a specific HTTP BLOCK rule
In the firewall dashboard:
1. Open Firewall → Rules → OPT1.
2. Add a rule and choose **Block**.
3. Select **IPv4** and **TCP**.
4. Set Source to the Kali test host (KALI_IP).
5. Set Destination to the Ubuntu server (UBUNTU_IP).
6. Set Destination port to **HTTP (80)**.
7. Enable logging and add a clear description, such as “Block Kali to Ubuntu HTTP test”.
8. Save and apply the rule.
9. Ensure the specific BLOCK rule is above any broader PASS rule that could match the same traffic.

## Step 4 — Retest from Kali
Run the same curl request:

    curl -v --connect-timeout 5 http://UBUNTU_IP:80/

The lab observation was that the request no longer connected after the TCP/80 BLOCK policy was applied. The exact terminal output and matching TCP log screenshot were not preserved in the current notes, so they should be attached before treating this as independently verified evidence.

## Expected vs observed
| Stage | Expected | Lab observation |
|---|---|---|
| Python HTTP server | Listen on Ubuntu TCP/80 | Server was started for the exercise |
| Baseline curl | Reach Ubuntu HTTP service | Directory listing was returned |
| After specific BLOCK | Kali cannot establish HTTP connection | Connection stopped after rule was applied |
| Firewall live log | Matching TCP/80 block entry | Screenshot/output still required |

## Troubleshooting checklist
If the result differs, verify the server is still running, the destination address is correct, the rule is on the ingress interface, protocol is TCP, destination port is 80, source/destination are correct, and the rule is above conflicting rules. Check the firewall log for the matching TCP event. Do not infer a TCP block from an unrelated ICMP log entry.

## Evidence checklist
- [ ] Ubuntu terminal showing the Python HTTP server running
- [ ] Kali baseline curl output showing the HTTP response
- [ ] OPT1 rule screenshot with the source, destination, TCP and port 80 fields
- [ ] Kali curl output after the BLOCK rule
- [ ] Matching firewall log entry showing the blocked TCP/80 attempt

## Key lesson
A port-specific rule can control one service without blocking every protocol or port between the same hosts. TCP/80 identifies the HTTP service in this lab; it does not represent all traffic from Kali to Ubuntu.
