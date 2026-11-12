# Cybersecurity_Week2project
My practical labs for Network Security at networklwalks
# Reconnaissance & Network Scanning Lab

A hands-on reconnaissance project covering passive and active information gathering, plus my first live network scan with Nmap / Zenmap. Completed as part of my training with **Networkwalks**.


---

## Liability Disclaimer

All activities in this project were performed only on systems and devices I own or where I had written permission. This material is for education and research only. Do not use anything here to break the law. Unauthorised access is a crime in most countries, even when nothing is damaged. Every action you take is your own responsibility.

---

## Operating Systems Used

- Kali Linux
- Windows

---

## Part 1: Reconnaissance Tools

| # | Tool | Purpose | Command |
|---|------|---------|---------|
| 1 | WHOIS | Domain registration details (owner, dates, name servers) | `whois example.com` |
| 2 | nslookup | Resolve the domain name to its IP address | `nslookup example.com` |
| 3 | curl -I | Read the HTTP response headers | `curl -I https://example.com` |
| 4 | WhatWeb | Fingerprint web technologies (server, CMS, plugins) | `whatweb example.com` |
| 5 | wafw00f | Detect a Web Application Firewall | `wafw00f https://example.com` |
| 6 | dnsrecon | Enumerate DNS records (NS, MX, SPF, TXT, SRV) | `dnsrecon -d example.com` |

### Findings

> Replace this section with your own results. Add a screenshot and one or two sentences of interpretation per tool.

| Tool | What I found |
|------|--------------|
| WHOIS | [registrar, creation/expiry dates, name servers] |
| nslookup | [IP address(es)] |
| curl -I | [status code, server header, missing security headers] |
| WhatWeb | [web server, CMS, technologies] |
| wafw00f | [WAF detected or not] |
| dnsrecon | [NS, MX, SPF/TXT records] |

---

## Part 2: Network Scanning with Nmap / Zenmap

My first live scan, run only against my own lab environment.

```bash
# Service and OS detection
nmap -sV -O -T3 <lab-target>

# Check SMB signing configuration
nmap -p445 --script smb2-security-mode <lab-target>
```

### What the scan identified

- **Open ports and services:** RPC, NetBIOS, SMB and WSDAPI
- **OS fingerprinting:** Windows 10 / 11
- **Uptime and running services**

### Key finding: SMB signing enabled but not required

SMB message signing was **enabled but not required**. The service supports signing but does not enforce it, so a client or attacker can still connect without it. This is the condition that makes **SMB relay attacks** possible.

**Lesson:** Cybersecurity isn't just about closing ports. It's about hardening what you have to keep open.

### Recommendations

- **Require SMB signing** through Group Policy: *Microsoft network server: Digitally sign communications (always)*.
- **Disable NetBIOS over TCP/IP** where it isn't needed.
- **Restrict SMB and RPC** with firewall rules so they are reachable only from trusted hosts.
- **Turn off WSD (Web Services for Devices)** discovery if the feature isn't needed.

---

## What I Learned

- How much information about an organisation is publicly visible without touching its systems
- How to read DNS, HTTP header and web fingerprint results
- How to scan a host with Nmap and interpret services and OS detection
- Why misconfigurations such as optional SMB signing matter as much as open ports

## Next Steps

- Packet analysis with Wireshark
- More Linux and Python for security tasks
- CCNA studies
- More Blue Team labs (log analysis, detection)

---
## Repository Structure


---
