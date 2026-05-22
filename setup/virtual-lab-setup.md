# 🔐 Security Lab Notes

A collection of hands-on attack and defense writeups performed inside a controlled virtual lab environment. Built for learning offensive security, network analysis, and penetration testing concepts.

> ⚠️ All attacks documented here are performed in an isolated lab environment. Never perform these attacks on networks or devices you don't own or have explicit permission to test.

---

## 🖥️ Lab Architecture

```
                    [OPNsense Firewall/Router]
                         192.168.1.1
                              |
              ________________|________________
             |                |                |
      [Kali Linux]    [Metasploitable 2]  [Ubuntu Server]
      192.168.1.192    192.168.1.190      192.168.1.106
      (Attacker)         (Victim 1)        (Victim 2)
```

---

## 🛠️ Lab Setup

| Component | Details |
|---|---|
| Hypervisor | Oracle VirtualBox |
| Firewall/Router | OPNsense 26.1 |
| Attacker | Kali Linux |
| Victim 1 | Metasploitable 2 |
| Victim 2 | Ubuntu Server 24.04 LTS |
| Network | VirtualBox Internal Network (LAB-NET) |

---

## 📂 Writeups

### Network Attacks
| # | Attack | Tools Used | Status |
|---|---|---|---|
| 01 | [MITM — ARP Spoofing](attacks/01-mitm-arp-spoofing.md) | arpspoof, Wireshark, netdiscover | ✅ Done |
| 02 | [vsftpd 2.3.4 Backdoor Exploit](attacks/02-vsftpd-exploit.md) | Metasploit, Wireshark | 🔄 Coming Soon |
| 03 | Telnet Credential Capture | Wireshark, arpspoof | 🔄 Coming Soon |
| 04 | DNS Spoofing | ettercap, Wireshark | 🔄 Coming Soon |
| 05 | FTP Credential Capture | Wireshark, Hydra | 🔄 Coming Soon |
| 06 | SSL Stripping | bettercap | 🔄 Coming Soon |

### Web Attacks
| # | Attack | Tools Used | Status |
|---|---|---|---|
| 07 | DVWA SQL Injection | sqlmap, Burp Suite | 🔄 Coming Soon |
| 08 | XSS via Network Layer | Burp Suite, Wireshark | 🔄 Coming Soon |

### Mobile Attacks
| # | Attack | Tools Used | Status |
|---|---|---|---|
| 09 | Android Reverse Shell (msfvenom) | msfvenom, Metasploit, Genymotion | 🔄 Coming Soon |

---

## 🔧 Tools Used

- **Kali Linux** — Attacker OS
- **Metasploit Framework** — Exploitation
- **Wireshark** — Packet analysis
- **arpspoof** — ARP spoofing
- **netdiscover** — Network scanning
- **Nmap** — Port scanning and fingerprinting
- **ettercap** — DNS spoofing
- **bettercap** — SSL stripping and traffic manipulation
- **Hydra** — Brute forcing
- **OPNsense** — Firewall and traffic monitoring

---

## 📌 Key Concepts Covered

- ARP protocol and ARP spoofing
- Man-in-the-Middle attacks
- Packet analysis with Wireshark
- Network reconnaissance
- Service exploitation
- Firewall rules and evasion
- Unencrypted vs encrypted protocols

---

## 🧠 Learning Resources

- [TryHackMe](https://tryhackme.com)
- [HackTheBox](https://hackthebox.com)
- [PortSwigger Web Academy](https://portswigger.net/web-security)
- [OPNsense Documentation](https://docs.opnsense.org)

---

## 📜 Disclaimer

All content in this repository is for **educational purposes only**. Performing these attacks on unauthorized systems is illegal under India's IT Act 2000 and similar laws worldwide. Always get written permission before testing any system you don't own.