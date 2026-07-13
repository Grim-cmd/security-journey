# Tcpdump: The Basics - TryHackMe Room Notes

**Room:** Tcpdump: The Basics  
**Difficulty:** Easy  
**Time:** 60min  

---

## Basic Options

| Command | Explanation |
|---------|-------------|
| `tcpdump -i INTERFACE` | Capture on specific interface |
| `tcpdump -w FILE` | Save to file (.pcap) |
| `tcpdump -r FILE` | Read from file |
| `tcpdump -c COUNT` | Limit number of packets |
| `tcpdump -n` | Don't resolve IPs |
| `tcpdump -nn` | Don't resolve IPs or ports |
| `tcpdump -v/-vv/-vvv` | Verbose output |

---

## Display Options

| Command | Explanation |
|---------|-------------|
| `-q` | Quick/quiet output |
| `-e` | Show MAC addresses |
| `-A` | Show ASCII data |
| `-xx` | Show hex data |
| `-X` | Show hex AND ASCII |

---

## Filters

### Host
```bash
tcpdump host 1.1.1.1
tcpdump src host 192.168.1.10
tcpdump dst host 8.8.8.8


Port
bash
tcpdump port 80
tcpdump src port 53
tcpdump dst port 443

Protocol
bash
tcpdump icmp
tcpdump udp
tcpdump tcp
Logical Operators
bash
# and - both conditions
tcpdump host 1.1.1.1 and tcp

# or - either condition
tcpdump udp or icmp

# not - exclude
tcpdump not tcp

TCP Flags
Flag	Meaning
tcp-syn	Start connection
tcp-ack	Acknowledge
tcp-fin	End connection
tcp-rst	Reset connection
bash
# SYN only
tcpdump "tcp[tcpflags] == tcp-syn"

# SYN set (at least)
tcpdump "tcp[tcpflags] & tcp-syn != 0"

# SYN or ACK
tcpdump "tcp[tcpflags] & (tcp-syn|tcp-ack) != 0"

Common Examples
bash
# Check interfaces
ip a s

# Basic capture
sudo tcpdump -i eth0 -c 50 -v

# Save to file
sudo tcpdump -i wlo1 -w data.pcap

# Read file
tcpdump -r traffic.pcap -n

# HTTPS traffic to example.com
tcpdump -i eth0 host example.com and tcp port 443 -w https.pcap

# SSH traffic
tcpdump -i any tcp port 22

# Count packets from IP
tcpdump -r traffic.pcap src host 192.168.124.1 -n | wc

# Size filters
tcpdump greater 100
tcpdump less 64

What I Learned
sudo required for capturing (not for reading)

-w saves packets, doesn't display them

-n speeds up capture (no DNS lookups)

-r reads .pcap files without sudo

Host/port/protocol filters narrow down traffic

TCP flags useful for analyzing handshakes

-X best for seeing both hex and ASCII

Quick Reference
Goal	Command
List interfaces	ip a s
Capture all	sudo tcpdump -i eth0
Save capture	sudo tcpdump -i eth0 -w file.pcap
Read capture	tcpdump -r file.pcap -n
Filter IP	tcpdump host 1.1.1.1
Filter port	tcpdump port 80
Filter protocol	tcpdump icmp
