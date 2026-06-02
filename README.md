# Automated VAPT Framework for Web Applications

> **92% OWASP Top 10 detection rate · 70% reduction in manual reporting effort · Formally adopted by SecureNest Technologies as standard assessment pipeline**

![Python](https://img.shields.io/badge/Python-3.9+-blue?style=flat-square&logo=python)
![Burp Suite](https://img.shields.io/badge/Burp%20Suite-Pro-orange?style=flat-square)
![OWASP](https://img.shields.io/badge/OWASP-Top%2010-red?style=flat-square)
![Docker](https://img.shields.io/badge/Docker-Supported-blue?style=flat-square&logo=docker)
![CVSS](https://img.shields.io/badge/CVSS-v3.1-critical?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## What It Does

A modular Python-based automation framework that integrates Burp Suite Pro API and OWASP ZAP to perform end-to-end web application security assessments. Automatically generates CVSS v3.1-scored PDF reports with both executive summaries and technical remediation guides — eliminating the manual reporting bottleneck in penetration testing engagements.

Tested across 10 DVWA and HackTheBox targets covering the full OWASP Top 10 vulnerability categories.

---

## Impact

| Metric | Result |
|--------|--------|
| OWASP Top 10 detection rate | 92% in controlled environments |
| Manual reporting time saved | 70% reduction |
| Organisations using this | SecureNest Technologies (standard pipeline) |
| Targets tested | 10+ (DVWA, HackTheBox) |
| Vulnerabilities covered | SQLi, XSS, CSRF, IDOR, Broken Auth, SSRF, XXE |

---

## Architecture

```
┌─────────────────────────────────────────────────┐
│              VAPT Automation Framework          │
├──────────────┬──────────────┬───────────────────┤
│  Recon       │  Scanning    │  Reporting        │
│  Module      │  Engine      │  Engine           │
│              │              │                   │
│  • Nmap      │  • Burp API  │  • CVSS v3.1      │
│  • Shodan    │  • OWASP ZAP │    Scoring        │
│  • Gobuster  │  • Nikto     │  • PDF Generation │
│  • Sublist3r │  • SQLmap    │  • Exec Summary   │
└──────────────┴──────────────┴───────────────────┘
                      │
              ┌───────▼────────┐
              │  Docker Runner │
              │  (Isolated)    │
              └────────────────┘
```

---

## Features

- **Automated reconnaissance** — subdomain enumeration, port scanning, technology fingerprinting
- **Active scanning** — Burp Suite Pro API integration + OWASP ZAP for deep vulnerability discovery
- **OWASP Top 10 coverage** — SQLi, XSS, CSRF, IDOR, Broken Authentication, SSRF, XXE, Access Control
- **CVSS v3.1 scoring** — automatic severity scoring on all findings
- **Dual-format reports** — executive-level PDF summary + full technical remediation guide
- **Docker support** — isolated scanning environment, consistent results across machines
- **Modular design** — each module runs independently or as part of the full pipeline

---

## Quick Start

### Prerequisites

```bash
# Clone the repo
git clone https://github.com/chythrabandaru/automated-vapt-framework
cd automated-vapt-framework

# Install dependencies
pip install -r requirements.txt

# Set up Burp Suite Pro API key in config
cp config.example.yaml config.yaml
# Edit config.yaml with your Burp Suite API key and target URL
```

### Run a Full Assessment

```bash
# Full pipeline (recon → scan → report)
python main.py --target https://target.com --mode full --output report.pdf

# Recon only
python main.py --target https://target.com --mode recon

# Scan only (after recon)
python main.py --target https://target.com --mode scan

# Generate report from existing scan data
python main.py --mode report --scan-data scans/latest.json --output report.pdf
```

### Docker

```bash
docker build -t vapt-framework .
docker run -v $(pwd)/reports:/app/reports vapt-framework --target https://target.com
```

---

## Sample Report Output

The framework generates:

1. **Executive Summary** — Risk rating, critical findings count, business impact, remediation priority
2. **Technical Report** — Per-vulnerability details: description, CVSS score, evidence, PoC steps, remediation code
3. **Remediation Tracker** — Spreadsheet mapping each finding to owner, priority, and fix deadline

> ⚠️ **Legal notice:** Only use against systems you own or have written permission to test. Unauthorised testing is illegal.

---

## Vulnerability Coverage

| OWASP Category | Detection Method | Automated? |
|----------------|-----------------|------------|
| A01 Broken Access Control | IDOR testing, IDOR fuzzer | ✅ |
| A02 Cryptographic Failures | Header analysis, SSL scan | ✅ |
| A03 Injection (SQLi, XSS) | SQLmap, Burp active scan | ✅ |
| A04 Insecure Design | Manual + heuristic checks | ⚠️ Partial |
| A05 Security Misconfiguration | Nikto, header checks | ✅ |
| A06 Vulnerable Components | CVE correlation, version detection | ✅ |
| A07 Auth Failures | Hydra, custom auth checks | ✅ |
| A08 SSRF | SSRF payload suite | ✅ |
| A09 Logging Failures | Response analysis | ⚠️ Partial |
| A10 CSRF | Token analysis, form testing | ✅ |

---

## Professional Context

This framework was developed during my role as Junior Penetration Tester at SecureNest Technologies, where it was formally adopted as the standard assessment and reporting pipeline across all client engagements.

Contributed to identifying 47 vulnerabilities across 12+ VAPT engagements, including 3 critical SQLi and XSS flaws, delivering a 60% reduction in client attack surface post-assessment.

---

## Author

**Chythra Bandaru** — Cybersecurity Professional | Penetration Tester  
[LinkedIn](https://linkedin.com/in/chythrabandaru) · [GitHub](https://github.com/chythrabandaru) · [TryHackMe Top 5% Global](https://tryhackme.com/p/chythrabandaru)
