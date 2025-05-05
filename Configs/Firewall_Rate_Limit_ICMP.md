# Firewall Rule: Rate-Limit Incoming ICMP Packets

This document shows how to configure firewall rules to mitigate ICMP-based DDoS attacks by limiting the rate of incoming ping (ICMP Echo Request) packets.

---

## Objective
Limit the rate of incoming ICMP Echo Requests (ping) to reduce exposure to ICMP Flood attacks (DDoS).

---

## Example 1: Using `iptables` on Linux

```bash
# Allow up to 1 ICMP ping per second (with burst up to 5)
sudo iptables -A INPUT -p icmp --icmp-type echo-request -m limit --limit 1/second --limit-burst 5 -j ACCEPT

# Drop excess pings\sudo iptables -A INPUT -p icmp --icmp-type echo-request -j DROP
```

**Explanation:**
- `--limit 1/second` means only 1 ping per second is allowed
- `--limit-burst 5` allows up to 5 at once (e.g., right after reboot)

To make it **persistent** (survives reboot):
- Save rules using `iptables-save > /etc/iptables/rules.v4`
- Or use a tool like `ufw` or `firewalld`

---

## Example 2: Using pfSense Firewall

1. Log in to the pfSense web UI
2. Go to **Firewall > Rules > WAN**
3. Click **Add (+)** to create a new rule
4. Configure the following:
   - **Action:** Pass
   - **Interface:** WAN
   - **Protocol:** ICMP
   - **ICMP Type:** Echo Request
   - **Advanced Options > State Type:** `None`
   - **Advanced Options > Max States:** `5`
   - **Advanced Options > Max New Connections / Second:** `1`
5. Add a second rule **below it** to block all other ICMP
6. Click **Save** and **Apply Changes**

This effectively rate-limits ICMP pings and drops excess requests.

---

## Why It Matters
ICMP floods are often used in DDoS attacks to overwhelm a target’s bandwidth. Rate-limiting keeps functionality (e.g., for diagnostics) while protecting against abuse.

---

## Optional Lab Challenge
- Set up a VM or test network
- Use `hping3` or `ping -f` to simulate ICMP flooding
- Watch how the firewall blocks excess traffic
- Monitor with `iftop`, `ntopng`, or Wireshark

---

**Author:** Charles J. Wasson  

