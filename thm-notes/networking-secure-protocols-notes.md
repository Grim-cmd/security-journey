# Networking Secure Protocols - TryHackMe Room Notes

**Room:** Networking Secure Protocols  
**Difficulty:** Easy  
**Time:** 60min  

---

## SSL/TLS History

| Year | Event |
|------|-------|
| 1995 | SSL 2.0 released (Netscape) |
| 1999 | TLS 1.0 developed (IETF) |
| 2018 | TLS 1.3 released |

> **TLS** provides **Confidentiality** & **Integrity** at Transport Layer

### TLS Certificate Process
1. Create **CSR** (Certificate Signing Request)
2. Submit to **CA** (Certificate Authority)
3. CA issues signed certificate
4. Server uses certificate to identify itself

---

## HTTP vs HTTPS

| | HTTP | HTTPS |
|---|------|-------|
| Port | 80 | 443 |
| Security | Cleartext | Encrypted (TLS) |
| Steps | TCP handshake → HTTP | TCP handshake → TLS → HTTP |

---

## Secure Protocol Ports

| Protocol | Standard Port | Secure Port |
|----------|---------------|-------------|
| HTTP | 80 | 443 (HTTPS) |
| SMTP | 25 | 465/587 (SMTPS) |
| POP3 | 110 | 995 (POP3S) |
| IMAP | 143 | 993 (IMAPS) |
| FTP | 21 | 990 (FTPS) |
| DNS | 53 | 853 (DoT) |

---

## SSH (Secure Shell)

- **Developed by:** Tatu Ylönen (1995)
- **Open Source:** OpenSSH (1999)
- **Port:** 22

### SSH Benefits
- Secure authentication (password, public key, 2FA)
- End-to-end encryption
- Integrity protection
- Tunneling (VPN-like)
- X11 forwarding (GUI apps)

```bash
ssh username@hostname
ssh 192.168.124.148 -X   # With GUI forwarding

SFTP vs FTPS
SFTP	FTPS
Based on	SSH	TLS/SSL
Port	22	990
Setup	Enable in SSH config	Requires certificate
Firewall	Easy (single port)	Tricky
bash
sftp username@hostname
get file.txt    # Download
put file.txt    # Upload

VPN (Virtual Private Network)
Connects offices/remote users securely over Internet

Encrypts all traffic through a tunnel

Can bypass geographical restrictions

Hides your IP address

Warning: VPNs illegal in some countries. Check local laws.

Three Security Approaches
Approach	Examples
TLS	HTTPS, SMTPS, POP3S, IMAPS
SSH	SSH, SFTP, SSH Tunneling
VPN	OpenVPN, IPsec, WireGuard

Quick Reference
Protocol	Port	Secure?
TELNET	23	❌ Cleartext
SSH	22	✅ Secure
HTTP	80	❌ Cleartext
HTTPS	443	✅ Secure
FTP	21	❌ Cleartext
IMAP	143	❌ Cleartext
