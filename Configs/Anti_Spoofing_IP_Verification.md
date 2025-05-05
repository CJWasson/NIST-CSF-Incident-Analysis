#  Source IP Verification: Anti-Spoofing for ICMP Packets

This guide covers how to implement source IP address verification on a firewall to defend against IP spoofing during ICMP-based attacks.

---

##  Objective
Prevent spoofed IP addresses from flooding your network with fake ICMP packets.

---

##  Example 1: Enable Reverse Path Filtering (Linux)

Reverse Path Filtering checks whether the source IP address of a packet is reachable via the interface it arrived on. If not, the packet is dropped as spoofed.

### Temporary (effective immediately):
```bash
echo 1 > /proc/sys/net/ipv4/conf/all/rp_filter
echo 1 > /proc/sys/net/ipv4/conf/default/rp_filter
```

### Permanent (survives reboot):
Add the following to `/etc/sysctl.conf`:
```bash
net.ipv4.conf.all.rp_filter=1
net.ipv4.conf.default.rp_filter=1
```
Then apply with:
```bash
sudo sysctl -p
```

** rp_filter Modes:**
- `0` = No filtering
- `1` = Strict filtering (recommended)
- `2` = Loose filtering (less secure)

---

## Example 2: pfSense Anti-Spoofing

In pfSense:
1. Go to **System > Advanced > Networking**
2. Check **"Enable reply-to on WAN rules"** (enables asymmetric route protection)
3. Under **Interfaces > WAN > Firewall rules**, enable **Bogon networks** blocking (to block fake/private IPs)

---

## Why It Matters
IP spoofing allows attackers to hide their identity and bypass basic filtering. Anti-spoofing ensures that traffic comes from valid, reachable sources — especially important during ICMP flood attacks.

---

## Lab Simulation
- Use `hping3` or Scapy to spoof source IP addresses
- Watch logs with `dmesg` or `journalctl -f`
- Verify that spoofed packets are silently dropped

---

**Author:** Charles J. Wasson

