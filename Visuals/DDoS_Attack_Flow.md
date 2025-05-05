#  DDoS Attack Flow Diagram

This guide visualizes how a Distributed Denial of Service (DDoS) attack unfolds - from attacker to overwhelmed target.

##  Flow Overview
```
                     ┌──────────────┐
                     │  Attacker   │
                     └────┬─────────┘
                          ▼
                 ┌──────────────────┐
                 │  Botnet Control  │◄────┐
                 └────┬─────────────┘     │
                      ▼                   │
         ┌──────────────────────┐         │
         │ Infected Devices     │◄────────┘
         │ (Zombies/Bots)       │
         └────┬─────────────┬───┘
              ▼             ▼
       ┌────────────┐ ┌────────────┐
       │  ICMP Flood│ │ TCP SYNs   │  ← Different DDoS traffic types
       └────┬───────┘ └────┬───────┘
            ▼              ▼
             ┌──────────────────────────────┐
             │ Target Server/Network Asset │
             │ (e.g., web server, firewall) │
             └──────────────────────────────┘
```

##  Breakdown
- **Attacker**: Coordinates the DDoS campaign, often anonymously
- **Botnet Controller**: Sends commands to zombie devices
- **Infected Devices (Zombies)**: Launch the flood of traffic
- **Traffic Types**: Commonly ICMP floods, TCP SYN floods, HTTP GET floods
- **Target**: Overwhelmed server, service, or network infrastructure

##  Goal
To overwhelm the target’s resources (bandwidth, CPU, memory), causing service outages or disruption.

---

📁 This diagram is part of the [NIST-CSF Incident Analysis](../README.md) repository.

