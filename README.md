<div align="center">

# NetGuard Toolkit 🛡️
### Modular Network Security & Reconnaissance Architecture

_A production-grade collection of automated defensive utilities engineered to discover cloud and network vulnerabilities._

[![Python](https://img.shields.io/badge/Language-Python%203-blue?style=flat-square&logo=python)](https://python.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](https://opensource.org/licenses/MIT)

</div>

---

## 🛠️ Project Overview
**NetGuard Toolkit** is a modular security testing framework designed for rapid host assessment and vulnerability discovery. It serves as the open-source networking foundation for **CloudGuard**—an upcoming AI-powered Cloud Security Posture Management (CSPM) platform built to eliminate enterprise infrastructure and misconfigurations.

---

## 📂 Core Utility Modules

| Script Name | Runtime | Security Capability |
| :--- | :--- | :--- |
| `subnet_calculator.py` | Python 3.x | Algorithmic analysis of CIDR boundaries and host scopes |
| `port_scanner.py` | Python 3.x | Multi-threaded ingress analysis targeting exposed, high-risk ports |
| `dns_lookup.py` | Python 3.x | Automated validation of core DNS infrastructure security records |
| `http_checker.py` | Python 3.x | Cryptographic handshake verification & HTTP security header evaluation |
| `firewall_analyser.py` | Python 3.x | Heuristic rule-parsing engine built to detect loose access policies |

---

## 🔒 Security Checks Explained

### 📡 Ingress Monitoring (`port_scanner.py`)
Scans network endpoints to ensure critical management ports aren't exposed directly to the public internet:
* **Port 22 (SSH):** Open to internet $\rightarrow$ **CRITICAL RISK**
* **Port 3306 (MySQL):** Exposed to public $\rightarrow$ **CRITICAL RISK**
* **Port 5432 (PostgreSQL):** Exposed to public $\rightarrow$ **CRITICAL RISK**

### 🌐 Web Cryptography Auditor (`http_checker.py`)
Analyzes target web servers for missing defensive configuration standards:
* **HSTS Header Missing:** $\rightarrow$ **HIGH RISK** (Allows protocol downgrade attacks)
* **X-Frame-Options Missing:** $\rightarrow$ **MEDIUM RISK** (Allows clickjacking vulnerabilities)
* **X-Content-Type-Options Missing:** $\rightarrow$ **MEDIUM RISK** (Allows MIME-sniffing exploits)

### 🧱 Policy Auditor (`firewall_analyser.py`)
* Evaluates active ingress security rules. Flags any rule opening high-value internal networks directly to `0.0.0.0/0` as a **CRITICAL** configuration failure.

---

## ⚙️ Quick Start & Usage

### 1. Installation
Clone the toolkit repository directly into your environment:
```bash
git clone [https://github.com/Prajwal18hikify/netguard-toolkit.git](https://github.com/Prajwal18hikify/netguard-toolkit.git)
cd netguard-toolkit
