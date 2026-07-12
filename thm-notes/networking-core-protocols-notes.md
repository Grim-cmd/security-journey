# Networking Core Protocols - TryHackMe Room Notes

**Room:** Networking Core Protocols  
**Difficulty:** Easy  
**Time:** 45min  

---

## Recon & Basics

| Command | What It Does | Key Output |
|---------|--------------|------------|
| `nslookup www.example.com` | Resolve domain to IP | A and AAAA records |
| `whois [domain]` | Check domain registration info | Registrant details and dates |
| `telnet [IP] 80` | Manual HTTP request | GET / HTTP/1.1 + Host header |
| `ftp [IP]` | Connect to FTP server | Login, ls, get files |

---

## Key Commands Used

| Command | Purpose |
|---------|---------|
| `nslookup` / `dig` | DNS lookup |
| `telnet [IP] [port]` | Manual connection to services (HTTP, SMTP, POP3, IMAP) |
| `ftp` | File transfer |
| `ping` / `traceroute` | Network diagnostics |

---

## What I Learned

- **DNS** resolves domain names to IP addresses using A, AAAA, MX, CNAME records
- **WHOIS** shows domain registration details
- **HTTP** is used for web browsing (GET, POST, etc.) on port 80/443
- **FTP** is for file transfer on port 21
- **SMTP** is for sending emails on port 25
- **POP3** is for downloading emails on port 110
- **IMAP** is for syncing emails across devices on port 143
- Many protocols are **text-based** so you can talk to them using `telnet`
- Each protocol has its own commands and default ports

---

## Common DNS Records

| Record | Description | Example |
|--------|-------------|---------|
| **A** | IPv4 address | 192.168.1.1 |
| **AAAA** | IPv6 address | 2001:db8::1 |
| **CNAME** | Canonical name (alias) | www → example.com |
| **MX** | Mail exchange | mail.example.com |
| **TXT** | Text records | SPF, DKIM, verification |

---

## Common Ports and Protocols

| Protocol | Port | Purpose | Text-Based? |
|----------|------|---------|-------------|
| HTTP | 80 | Web browsing | ✅ Yes |
| HTTPS | 443 | Secure web browsing | ❌ Encrypted |
| FTP | 21 | File transfer | ✅ Yes |
| FTP Data | 20 | File transfer data | ✅ Yes |
| SMTP | 25 | Sending emails | ✅ Yes |
| POP3 | 110 | Downloading emails | ✅ Yes |
| IMAP | 143 | Syncing emails | ✅ Yes |
| DNS | 53 | Domain resolution | ❌ Binary |
| SSH | 22 | Secure shell | ❌ Encrypted |
| Telnet | 23 | Remote access | ✅ Yes |

---

## Manual Protocol Communication Examples

### HTTP (Port 80)
```bash
telnet example.com 80
GET / HTTP/1.1
Host: example.com
[press Enter twice]

# Response:
HTTP/1.1 200 OK
Content-Type: text/html
...

SMTP (Port 25)
telnet mail.example.com 25
HELO client.example.com
MAIL FROM: <sender@example.com>
RCPT TO: <recipient@example.com>
DATA
Subject: Test Email

This is a test email.
.
QUIT

FTP (Port 21)
telnet ftp.example.com 21
USER username
PASS password
LIST
RETR file.txt
QUIT

DNS Lookup Commands
# Basic DNS lookup
nslookup google.com
nslookup 8.8.8.8  # Reverse lookup

# Detailed DNS with dig
dig google.com
dig google.com A
dig google.com MX
dig google.com ANY

# WHOIS lookup
whois google.com
whois example.com

Quick Reference: Protocol Purpose
Protocol	Function
DNS	"Phonebook" for the internet
HTTP/S	Web browsing
FTP	Uploading/downloading files
SMTP	Sending email (push)
POP3	Downloading email (pull, deletes from server)
IMAP	Syncing email (pull, keeps on server)

Key Takeaway
Most application layer protocols are text-based and human-readable, which means you can interact with them manually using telnet or nc (netcat)! This is great for troubleshooting and understanding how these protocols work at a fundamental level.
