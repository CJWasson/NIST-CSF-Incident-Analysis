# NIST-CSF Incident Analysis

This project contains a structured incident report based on the **NIST Cybersecurity Framework (CSF)**. The scenario involves an **ICMP-based Distributed Denial of Service (DDoS) attack** that disrupted internal network services within a multimedia organization.

##  Project Overview

- **Framework Used:** NIST Cybersecurity Framework  
- **Incident Type:** ICMP Flood (DDoS)  
- **Organization Type:** Multimedia (Web Design & Marketing)  
- **Duration of Incident:** ~2 hours  
- **Impacted Services:** Internal email, shared drives, and printing systems  

The report outlines how the organization applied the five NIST CSF functions:  
`Identify → Protect → Detect → Respond → Recover`

##  Repository Structure

```
NIST-CSF-Incident-Analysis/
│
├── Docs/
│   └── Incident_Report_NIST.pdf          # Polished PDF version
│   └── Incident_Scenario_Description.pdf # Attack scenario context
│
├── Configs/
│   └── Firewall_Rate_Limit_ICMP.md       # ICMP flood firewall example
│   └── Anti_Spoofing_IP_Verification.md  # Reverse path filtering
│   └── ICMP_Monitoring_RealWorld_Tools.md# Tools to detect ICMP spikes
│   └── IDS_IPS_ICMP_Snort_Rules.md       # Snort detection examples
│
├── README.md                             # This file
```

##  Tools & Techniques Used

- NIST CSF for incident response modeling
- ICMP traffic analysis and detection strategies
- Firewall configuration and spoofed IP detection
- IDS/IPS deployment planning
- Recovery and business continuity process

##  Learning Objectives

- Practice identifying, analyzing, and responding to cybersecurity threats using structured frameworks
- Demonstrate knowledge of DDoS mitigation strategies
- Apply security hardening, detection, and incident handling procedures

##  Why I Built This

As a lifelong learner transitioning into cybersecurity, I built this project to practice applying the NIST Cybersecurity Framework (CSF) to a real-world incident scenario, a simulated ICMP-based DDoS attack.

My goal was not only to understand the theory, but to get hands-on with the tools, commands, and configurations used by professionals. I’ve documented each solution in a way that other learners can follow step-by-step, just like I would have wanted when I was starting out.

This project reflects who I am: someone who learns by doing, takes time to understand the why behind every step, and wants to help others on the same path.

---

**Prepared by:** Charles J. Wasson


