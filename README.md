# 🛡️ NetGuard Toolkit

> **Professional Network Security CLI** — Subnet analysis, port scanning, DNS inspection, HTTPS auditing, and firewall policy review in one unified toolkit.

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue?style=flat-square&logo=python)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](LICENSE)
[![Security](https://img.shields.io/badge/Security-Tools-red?style=flat-square)](https://github.com/Prajwal18hikify/netguard-toolkit)
[![Phase](https://img.shields.io/badge/CloudGuard-Phase%201-orange?style=flat-square)](https://github.com/Prajwal18hikify)

-----

## 📖 Overview

**NetGuard Toolkit** is a command-line network security suite built for engineers who need fast, reliable security analysis without enterprise-tool overhead. It bundles five focused security tools into one clean CLI — identify misconfigurations, open ports, DNS issues, missing security headers, and dangerous firewall rules in seconds.

> Built as part of the [CloudGuard 150-Day AI Cloud Security Journey](https://github.com/Prajwal18hikify) — Phase 1: Foundations.

-----

## 🔧 Tools Included

|Tool               |File                  |Purpose                                      |
|-------------------|----------------------|---------------------------------------------|
|🌐 Subnet Calculator|`subnet_calculator.py`|Analyses any network — CIDR, hosts, broadcast|
|🔍 Port Scanner     |`port_scanner.py`     |Finds dangerous open ports on any host       |
|🔎 DNS Lookup       |`dns_lookup.py`       |Checks DNS records for misconfigurations     |
|🔒 HTTP Checker     |`http_checker.py`     |Audits HTTPS config and security headers     |
|🧱 Firewall Analyser|`firewall_analyser.py`|Detects dangerous firewall rules (0.0.0.0/0) |
|🚀 Unified CLI      |`netguard.py`         |Runs all tools from one command              |

-----

## ⚠️ Risk Severity Levels

|Level         |Meaning                                           |
|--------------|--------------------------------------------------|
|🔴 **CRITICAL**|Immediate action required — exposed attack surface|
|🟠 **HIGH**    |Serious misconfiguration — fix within 24 hours    |
|🟡 **MEDIUM**  |Security weakness — schedule remediation          |
|🟢 **LOW**     |Best practice gap — address in next cycle         |

-----

## ⚙️ Quick Start & Usage

### 1. Installation

**Requirements:** Python 3.8+

```bash
# Clone the repository
git clone https://github.com/Prajwal18hikify/netguard-toolkit
cd netguard-toolkit

# Install dependencies
pip install -r requirements.txt
```

**Dependencies (`requirements.txt`):**

```
requests
dnspython
colorama
```

-----

### 2. Run Individual Tools

#### 🌐 Subnet Calculator

Analyses a network range — shows network address, broadcast, usable hosts, and CIDR breakdown.

```bash
python subnet_calculator.py 192.168.1.0/24
```

**Sample Output:**

```
[INFO] Network:     192.168.1.0
[INFO] Broadcast:   192.168.1.255
[INFO] Subnet Mask: 255.255.255.0
[INFO] Usable Hosts: 254
[INFO] Host Range:  192.168.1.1 — 192.168.1.254
```

-----

#### 🔍 Port Scanner

Scans a host for open ports. Flags dangerous services (Telnet, FTP, RDP, SMB) as HIGH or CRITICAL.

```bash
python port_scanner.py 192.168.1.1
python port_scanner.py 192.168.1.1 --ports 1-1024
```

**Sample Output:**

```
[OPEN]     Port 22  — SSH (acceptable)
[CRITICAL] Port 23  — Telnet detected — unencrypted protocol, replace with SSH
[HIGH]     Port 445 — SMB open — high risk of ransomware lateral movement
[OPEN]     Port 80  — HTTP (recommend redirect to HTTPS)
```

-----

#### 🔎 DNS Lookup

Resolves all DNS record types for a domain. Flags missing SPF, DMARC, and DNSSEC.

```bash
python dns_lookup.py google.com
python dns_lookup.py example.com --type MX
```

**Sample Output:**

```
[INFO]  A Record:     142.250.80.46
[INFO]  MX Record:    smtp.google.com (priority 10)
[HIGH]  SPF Record:   Missing — domain vulnerable to email spoofing
[HIGH]  DMARC Record: Missing — no protection against phishing
```

-----

#### 🔒 HTTP Checker

Audits an HTTPS endpoint for TLS configuration and security headers.

```bash
python http_checker.py https://example.com
```

**Sample Output:**

```
[PASS]   HTTPS:                  Enabled
[PASS]   TLS Version:            TLS 1.3
[HIGH]   HSTS Header:            Missing — allows protocol downgrade attacks
[MEDIUM] X-Frame-Options:        Missing — allows clickjacking vulnerabilities
[MEDIUM] X-Content-Type-Options: Missing — allows MIME-sniffing exploits
[HIGH]   Content-Security-Policy: Missing — no XSS protection
```

-----

#### 🧱 Firewall Analyser

Evaluates firewall/security group rules. Flags any rule opening high-value ports to `0.0.0.0/0` as CRITICAL.

```bash
python firewall_analyser.py rules.json
```

**`rules.json` format:**

```json
[
  {"port": 22, "protocol": "TCP", "source": "0.0.0.0/0", "description": "SSH open to world"},
  {"port": 443, "protocol": "TCP", "source": "0.0.0.0/0", "description": "HTTPS public"},
  {"port": 3306, "protocol": "TCP", "source": "0.0.0.0/0", "description": "MySQL exposed"}
]
```

**Sample Output:**

```
[CRITICAL] Port 22  (SSH)   — open to 0.0.0.0/0 — restrict to known IPs immediately
[PASS]     Port 443 (HTTPS) — public access acceptable
[CRITICAL] Port 3306 (MySQL) — open to 0.0.0.0/0 — database directly internet-exposed
```

-----

### 3. Run All Tools — Unified CLI

Run a full security audit on a target with one command:

```bash
python netguard.py --target 192.168.1.0/24
python netguard.py --url https://example.com
python netguard.py --domain example.com
python netguard.py --rules rules.json
python netguard.py --full --target 192.168.1.1 --url https://example.com --domain example.com
```

**Full Audit Sample Output:**

```
╔══════════════════════════════════════════╗
║       NETGUARD SECURITY REPORT           ║
║       Target: 192.168.1.1                ║
╚══════════════════════════════════════════╝

[SUBNET]
  Network: 192.168.1.0 | Hosts: 254

[PORT SCAN]
  [CRITICAL] Port 23 — Telnet open
  [HIGH]     Port 445 — SMB open

[DNS]
  [HIGH] DMARC missing

[HTTP]
  [HIGH]   HSTS missing
  [MEDIUM] X-Frame-Options missing

[FIREWALL]
  [CRITICAL] Port 3306 open to 0.0.0.0/0

═══════════════════════════════════════════
SUMMARY: 2 CRITICAL | 3 HIGH | 1 MEDIUM
═══════════════════════════════════════════
```

-----

## 📁 Repository Structure

```
netguard-toolkit/
├── subnet_calculator.py    # CIDR + network analysis
├── port_scanner.py         # TCP port scanning + risk flagging
├── dns_lookup.py           # DNS record inspection
├── http_checker.py         # HTTPS + security headers audit
├── firewall_analyser.py    # Firewall rule risk evaluation
├── netguard.py             # Unified CLI — runs all tools
├── requirements.txt        # Python dependencies
├── rules.json              # Sample firewall rules for testing
└── README.md               # This file
```

-----

## 🧪 Testing

```bash
# Test against safe public targets
python port_scanner.py scanme.nmap.org
python http_checker.py https://google.com
python dns_lookup.py cloudflare.com

# Test firewall analyser with sample rules
python firewall_analyser.py rules.json
```

> ⚠️ **Legal Notice:** Only scan systems you own or have explicit written permission to test. Unauthorized scanning is illegal.

-----

## 🗺️ Roadmap

- [x] Phase 1 — Individual tools (Days 1–5)
- [x] Phase 1 — Unified CLI (Days 6–7)
- [ ] Phase 2 — AWS IAM + S3 + EC2 checks
- [ ] Phase 3 — CIS Benchmark mapping
- [ ] Phase 4 — CloudGuard SaaS dashboard
- [ ] Phase 5 — AI-powered remediation (Claude API)

-----

## 🤝 Contributing

Pull requests welcome. For major changes, open an issue first.

1. Fork the repo
1. Create a feature branch: `git checkout -b feature/your-feature`
1. Commit changes: `git commit -m 'Add: your feature'`
1. Push: `git push origin feature/your-feature`
1. Open a Pull Request

-----

## 👤 Author

**Prajwal CK**

- GitHub: [@Prajwal18hikify](https://github.com/Prajwal18hikify)
- Building: CloudGuard — AI-Powered Cloud Security Scanner
- Journey: Biotechnology → AI Cloud Security Engineer (150 Days)

-----

## 📄 License

MIT License — free to use, modify, and distribute.

-----

> *Part of the CloudGuard 150-Day Journey — Phase 1 of 6*
