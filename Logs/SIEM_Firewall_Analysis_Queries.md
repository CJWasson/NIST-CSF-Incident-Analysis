#  SIEM Query Examples for Firewall Misconfiguration Analysis (pfSense)

This walkthrough includes example pfSense firewall logs and matching SIEM search queries for detecting ICMP flood behavior and confirming firewall rule effectiveness.

---

##  Use Case: Misconfigured Firewall (pfSense)
The firewall was improperly configured to allow unrestricted inbound ICMP traffic, leading to a successful ICMP-based DDoS attack.

My goal in the SIEM:  
- Detect the attack  
- Confirm absence/presence of rate-limiting rules  
- Visualize or alert on anomaly patterns

---

##  Sample pfSense Log Entry (Syslog)
```
May 5 02:14:02 pfSense firewall: [UFW BLOCK] IN=em0 OUT= MAC=00:0c:29:a6:6c:75 SRC=192.0.2.12 DST=10.0.0.15 LEN=84 TOS=0x00 TTL=245 ID=53104 PROTO=ICMP TYPE=8 CODE=0 ID=43432 SEQ=1
```

##  Splunk Query Example
```splunk
index=firewall sourcetype=pfsense_log proto=ICMP src_ip!=10.0.0.0/8 | stats count by src_ip, dest_ip
```
**Purpose:** See which external IPs are targeting your internal servers

---

##  Confirm Firewall Rule Effectiveness
### Splunk
```splunk
index=firewall action=block proto=ICMP | timechart span=1m count
```
**Purpose:** Track blocks per minute — did rate limiting start working?

---

##  Investigation Enhancements
- Correlate with Snort alerts (signature-based detection)
- Alert when ICMP traffic > X per minute from a single source
- Visualize top sources by volume over time

---

 This file supports the root incident (ICMP flood) and ties directly to misconfiguration and mitigation.
