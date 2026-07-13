# Wireshark: The Basics - TryHackMe Room Notes

**Room:** Wireshark: The Basics  
**Difficulty:** Easy  
**Time:** 60min  

---

## Key Actions

| Action | Purpose |
|--------|---------|
| Open pcap file | Load captured traffic |
| Right click packet | Apply filter or follow stream |
| Display Filter | Filter traffic (http, ip.addr, tcp.port) |
| Follow TCP/UDP Stream | Reconstruct full conversation |
| Apply as Column | Add fields to packet list |
| Expert Info | See warnings and errors |

---

## Wireshark Interface

### 3 Main Panes
1. **Packet List** - Top (summary of all packets)
2. **Packet Details** - Middle (protocol breakdown)
3. **Packet Bytes** - Bottom (raw hex/ASCII)

### OSI Layer Display
Packets show layers from **Frame → Application Data**

---

## Useful Display Filters

| Filter | Purpose |
|--------|---------|
| `http` | Show only HTTP traffic |
| `dns` | Show only DNS traffic |
| `ip.addr == 192.168.1.1` | Traffic to/from specific IP |
| `tcp.port == 80` | Traffic on port 80 |
| `http.request.method == GET` | HTTP GET requests |
| `icmp` | Show only ping traffic |
| `arp` | Show ARP traffic |

---

## What I Learned

- **Color coding** - Packets colored by protocol for quick identification
- **Follow Stream** - See full HTTP/FTP/SMTP conversations
- **Display filters** - Remove noise, focus on specific traffic
- **Right-click power** - Apply filters, follow streams, mark packets
- **Protocol hierarchy** - Shows breakdown of traffic types
- **Expert Info** - Warnings, errors, and notes about packets
- **Wireshark shows packets in OSI layers** from Frame to Application data
- **Good for learning protocols** and troubleshooting network issues

---

## Common Workflow

1. Open pcap file
2. Check Protocol Hierarchy (Statistics → Protocol Hierarchy)
3. Apply display filters to narrow down
4. Right-click interesting packets → Follow Stream
5. Analyze payload

---

## Example Filters

```bash
# Filter by IP
ip.addr == 10.10.10.1

# Filter by port
tcp.port == 443

# Filter by protocol
http or dns or icmp

# Filter HTTP methods
http.request.method == POST

# Exclude traffic
!arp


Quick Reference
Color	Usually Means
Green	HTTP/Web traffic
Blue	DNS traffic
Yellow	Routing protocols
Red	TCP errors/resets
