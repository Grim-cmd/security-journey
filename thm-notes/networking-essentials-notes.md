# Networking Essentials - TryHackMe Room Notes

**Room:** Networking Essentials  
**Difficulty:** Easy  
**Time:** 60min  

---

## Recon & Basics

| Command | What It Does | Key Output |
|---------|--------------|------------|
| `telnet` / `tshark` | Capture and see DHCP process | DORA (Discover, Offer, Request, ACK) |
| `ping [IP]` | Test connectivity | Round trip time and packet loss |
| `traceroute [domain]` | Show path to destination | List of routers along the way |
| `arp` | See ARP requests and replies | MAC address resolution |

---

## Key Commands Used

| Command | Purpose |
|---------|---------|
| `ping` | Check if host is alive using ICMP Echo |
| `traceroute` | Discover routers between you and target |
| `ifconfig` / `ip a` | Check IP configuration |
| `tshark` / `tcpdump` | Capture and analyse network traffic |

---

## What I Learned

- **DHCP** uses **DORA** process to automatically give IP address, gateway, and DNS to devices
  - **D**iscover → **O**ffer → **R**equest → **A**CK
- **ARP** resolves IP address to MAC address on local network
- **ARP request** is broadcasted to `ff:ff:ff:ff:ff:ff`
- **ICMP** is used for ping and traceroute
- **Ping** sends ICMP Echo Request and gets Echo Reply
- **Traceroute** uses TTL and ICMP Time Exceeded messages
- **NAT** allows many private IPs to share one public IP
- **Private IP ranges** are important to remember

---

## DHCP DORA Process

| Step | Name | Description |
|------|------|-------------|
| 1 | **D**iscover | Client broadcasts "Who has an IP for me?" |
| 2 | **O**ffer | DHCP server offers an IP address |
| 3 | **R**equest | Client requests the offered IP |
| 4 | **A**CK | Server acknowledges and assigns the IP |

---

## Common Protocols and Their Functions

| Protocol | Function | Port(s) |
|----------|----------|---------|
| DHCP | Automatic IP assignment | UDP 67/68 |
| ARP | IP to MAC resolution | Layer 2 |
| ICMP | Error reporting, ping, traceroute | Layer 3 |
| DNS | Domain name to IP resolution | UDP/TCP 53 |
| NAT | Private to public IP translation | - |

---

## Example Commands

```bash
# Check connectivity
ping 8.8.8.8
ping -c 4 google.com

# Trace route to destination
traceroute google.com
traceroute -n 8.8.8.8  # Skip DNS resolution

# View ARP table
arp -a
ip neigh show

# Capture DHCP traffic
sudo tshark -i eth0 -Y "bootp" -f "port 67 or port 68"

# Capture ARP traffic
sudo tshark -i eth0 -Y "arp"

# Network interface info
ifconfig
ip a
ip route show 


Private IP Ranges (RFC 1918)
Range	CIDR	Usage
10.0.0.0 - 10.255.255.255	10.0.0.0/8	Large networks
172.16.0.0 - 172.31.255.255	172.16.0.0/12	Medium networks
192.168.0.0 - 192.168.255.255	192.168.0.0/16	Small/home networks
Remember: These IPs are NOT routable on the internet!

Networking Layers Reference
Layer	Name	Protocols/Concepts
5	Application	DHCP, DNS, HTTP
4	Transport	TCP, UDP
3	Network	IP, ICMP, ARP
2	Data Link	MAC addresses, frames
1	Physical	Cables, Wi-Fi
