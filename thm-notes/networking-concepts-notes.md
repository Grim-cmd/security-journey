# Networking Concepts - TryHackMe Room Notes

**Room:** Networking Concepts  
**Difficulty:** Easy  
**Time:** 60min  

---

## Recon & Basics

| Command | What It Does | Key Output |
|---------|--------------|------------|
| `telnet 10.49.185.38 7` | Connect to echo server | Echoes back whatever you type |
| `telnet 10.49.185.38 13` | Connect to daytime server | Returns current date and time |
| `telnet 10.49.185.38 80` | Connect to web server | Can send manual HTTP request (GET / HTTP/1.1) |

---

## Key Commands Used

| Command | Purpose |
|---------|---------|
| `telnet [IP] [port]` | Connect to any TCP port manually |
| `ifconfig` / `ip a` | Check network configuration and IP address |

---

## What I Learned

- **Telnet** lets you connect to any open TCP port and talk to the service directly
- **Echo server** on port 7 just repeats what you send
- **Daytime server** on port 13 gives current time and closes connection
- You can even talk to **HTTP server** on port 80 using manual GET request
- **Encapsulation** is how data gets headers added at each layer (Application → Transport → Network → Link)
- **OSI Model** has 7 layers. Very important to remember
- **TCP** is reliable, connection-oriented with 3-way handshake
- **UDP** is fast, connectionless, no guarantee of delivery
- **Private IP ranges**: 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16
- **IP address + Port number** = unique process on a machine

---

## OSI Model Layers (7 Layers)

| Layer | Name | Description |
|-------|------|-------------|
| 7 | Application | User interface (HTTP, FTP, DNS) |
| 6 | Presentation | Data formatting, encryption |
| 5 | Session | Connection establishment |
| 4 | Transport | TCP/UDP, port numbers |
| 3 | Network | IP addressing, routing |
| 2 | Data Link | MAC addresses, frames |
| 1 | Physical | Cables, bits |

> **Mnemonics**: "Please Do Not Throw Sausage Pizza Away" (Bottom to Top)
> Or "All People Seem To Need Data Processing" (Top to Bottom)

---

## Common Ports

| Port | Protocol | Service |
|------|----------|---------|
| 7 | TCP | Echo |
| 13 | TCP | Daytime |
| 20/21 | TCP | FTP |
| 22 | TCP | SSH |
| 23 | TCP | Telnet |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 80 | TCP | HTTP |
| 443 | TCP | HTTPS |

---

## Example Telnet Commands

```bash
# Connect to echo server
telnet 10.49.185.38 7
> Hello
Hello

# Connect to daytime server
telnet 10.49.185.38 13
> Sun Jul 5 14:32:15 2026

# Manual HTTP request
telnet 10.49.185.38 80
GET / HTTP/1.1
Host: example.com

# Response will show HTML content
