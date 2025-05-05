#  IDS/IPS Rules: Detecting ICMP-Based Attacks with Snort

This guide walks through how to write Snort (or Suricata-compatible) rules to detect suspicious ICMP traffic and flag potential ICMP-based DDoS attacks.

---

##  Objective
Use signature-based detection to identify ICMP flood patterns, malformed packets, or abnormal traffic frequency.

---

##  Snort Rule Example: ICMP Flood Detection

```snort
alert icmp any any -> any any (
    msg:"ICMP Flood Detected";
    itype:8;
    dsize:0;
    detection_filter:track by_src, count 20, seconds 1;
    sid:1000001;
    rev:1;
)
```

###  Breakdown
- `icmp` — protocol
- `itype:8` — ICMP Echo Request
- `dsize:0` — payload size check (optional, zeroed packets are suspicious)
- `detection_filter:` — triggers if 20 pings come from same source in 1 second
- `sid` — Signature ID (custom range starts at 1,000,000)

---

##  Rule Example: Oversized ICMP Packets (Malicious Ping of Death)

```snort
alert icmp any any -> any any (
    msg:"Oversized ICMP Packet";
    dsize:>1024;
    itype:8;
    sid:1000002;
    rev:1;
)
```

---

##  How to Deploy in Snort
1. Open your rules file (e.g., `local.rules`)
2. Paste the rule at the bottom
3. Update `snort.conf` to include `local.rules`
4. Restart Snort:
```bash
sudo snort -A console -q -c /etc/snort/snort.conf -i eth0
```
5. Generate ICMP traffic with `ping -f` or `hping3` to test detection

---

##  Why It Matters
Signature-based detection gives your network the ability to immediately spot known attack patterns — and alert security staff to take action. These rules help defend against ICMP floods and malformed packets often used in DDoS or evasion attacks.

---

##  Lab Simulation
- Use `ping -f` to trigger flood detection
- Use `ping -s 2000` to simulate oversized ping payload
- Watch Snort logs to verify rule match alerts

---

##  Learner Notes
- Writing Snort rules helped me understand how packet matching works at the protocol level.
- The `detection_filter` was new to me, but it's powerful for rate-limiting alerts by source.
- I still plan to explore how Suricata handles threshold rules and experiment with alert tuning in the future.

---

**Author:** Charles J. Wasson  

