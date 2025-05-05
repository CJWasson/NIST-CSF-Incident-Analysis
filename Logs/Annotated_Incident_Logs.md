#  Annotated Incident Logs: DDoS Detection Example

These sample logs simulate traffic observed during the ICMP-based DDoS attack. Each entry is annotated to help identify red flags, abnormal behavior, and attack indicators.

---

##  Sample Syslog Snippet (Firewall)
```
May 5 02:14:02 pfSense firewall: [UFW BLOCK] IN=eth0 OUT= MAC=00:0c:29:a6:6c:75 SRC=192.0.2.12 DST=10.0.0.15 LEN=84 TOS=0x00 PREC=0x00 TTL=245 ID=53104 PROTO=ICMP TYPE=8 CODE=0 ID=43432 SEQ=1
```
**Explanation:**
- `SRC=192.0.2.12` → Suspicious source IP
- `PROTO=ICMP TYPE=8` → Echo request (ping)
- `LEN=84` repeated hundreds of times in short bursts → potential flood pattern
- Blocked by UFW (uncomplicated firewall)

 **Flagged as potential part of ICMP flood**

---

##  IDS Alert (Snort)
```
[**] [1:1000002:1] ICMP flood attempt detected [**]
[Priority: 2] 
04/21-02:14:07.221954 192.0.2.12 -> 10.0.0.15
ICMP TTL:245 TOS:0x0 ID:5612 IpLen:20 DgmLen:84
Type:8  Code:0  ID:43432   Seq:1  ECHO
```
**Explanation:**
- Snort signature `1:1000002:1` is custom-defined for ICMP flood
- Multiple identical echo requests (`Type:8`) over short time span
- Alert priority 2 = Medium severity

 **Confirmed detection by IDS rule**

---

##  Network Monitoring Log (ntopng / Wireshark excerpt)
```
02:14:07 IP 192.0.2.12 > 10.0.0.15: ICMP echo request, id 43432, seq 1, length 64
02:14:07 IP 192.0.2.12 > 10.0.0.15: ICMP echo request, id 43432, seq 2, length 64
02:14:07 IP 192.0.2.12 > 10.0.0.15: ICMP echo request, id 43432, seq 3, length 64
...
02:14:08 IP 192.0.2.13 > 10.0.0.15: ICMP echo request, id 43912, seq 1, length 64
```
**Explanation:**
- Packet flood from multiple spoofed source IPs
- High frequency within same second = anomaly
- Matches signature of classic ICMP DoS

 **Cross-referenced against Snort and firewall logs**

---

##  Summary: How This Helped
| Tool          | Detection Role                  |
|---------------|----------------------------------|
| pfSense       | First-layer packet filtering     |
| Snort         | Alerting on ICMP flood behavior  |
| ntopng/Wireshark | Visual confirmation of burst   |

---

 This file supports the full incident narrative and helps reinforce how each system logs, flags, and supports DDoS detection.


