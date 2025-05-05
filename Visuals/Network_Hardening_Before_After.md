#  Network Hardening: Before vs After

This layout shows a side-by-side comparison of a flat, unprotected network versus a segmented, hardened network.

---

##  Before Hardening
```
+------------------+
|  Internet        |
+------------------+
        |
        ▼
+------------------+
| Router           |
+------------------+
        |
        ▼
+------------------+     +------------------+
| Switch           |────▶| All internal hosts|
+------------------+     +------------------+
        ▼
    No firewall, no segmentation, all ports open
```

**Risks:**
- No access control
- No traffic filtering
- Flat network allows easy lateral movement
- Susceptible to port scans, malware spread, and DDoS impact

---

##  After Hardening
```
+------------------+
|  Internet        |
+------------------+
        |
        ▼
+------------------------+
| Router (Edge ACLs)     |
+------------------------+
        |
        ▼
+------------------------+
|  pfSense Firewall       |
|  - ICMP rate limit      |
|  - Allow TCP 443 only   |
|  - IDS/IPS w/ Snort     |
+------------------------+
        |
        ▼
+---------------------+         +---------------------+
|  Internal Switch     |───────▶| Application Servers |
+---------------------+         +---------------------+
        |                            ▲
        ▼                            │
+---------------------+    +---------------------+
| Workstations VLAN    |    | Database VLAN       |
+---------------------+    +---------------------+
        ▲                            ▲
        |                            |
  DHCP/IP rules + VLAN segmentation  |
             -------------------------
```

**Security Improvements:**
- Firewall enforces access control and logging
- VLANs isolate departments and services
- IDS/IPS inspects and blocks suspicious traffic
- ICMP flood mitigation through rate limiting

---

 For full implementation, see the [Incident Report](../Docs/Incident_Report_NIST.pdf) and walkthroughs in the `Configs/` folder.
