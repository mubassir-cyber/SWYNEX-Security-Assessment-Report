# SWYNEX Security Assessment Report

**A consolidated defensive security assessment of an authorized lab environment (OWASP Juice Shop and local network traffic)**

**Author:** Mubassir, Security Intern, SWYNEX Technologies | **Task:** 4, Security Assessment Report

---

## Project Overview

This repository contains my **Task 4** submission for the SWYNEX Technologies internship. It combines the findings from my earlier lab tasks into one professional security assessment report:

- **Task 1:** Security Fundamentals Assessment
- **Task 2:** Network Security Analysis
- **Task 3:** Web Security Review

The full report is in [`report/Security-Assessment-Report.pdf`](report/Security-Assessment-Report.pdf). It contains an executive summary, methodology, findings, risk ratings, evidence and remediation recommendations.

## Scope and Authorization

All testing was performed in an isolated lab that I own and control:

- Target: **OWASP Juice Shop**, an intentionally vulnerable training application, running in Docker on `localhost:3000` inside a Kali Linux VM.
- Network analysis used traffic I generated myself, plus an Nmap scan of my own loopback interface.
- No third-party or production systems were accessed, scanned or attacked.

## Findings Summary

| ID | Finding | OWASP Category | Risk |
|---|---|---|---|
| F1 | SQL injection: authentication bypass | A03:2021 Injection | **Critical** |
| F2 | Sensitive file exposure at `/ftp/` | A01:2021 Broken Access Control | **High** |
| F3 | Credentials and cookies sent in cleartext HTTP | A02:2021 Cryptographic Failures | **High** |
| F4 | Detectable TCP SYN port scan pattern | Detection and monitoring | **High** |
| F5 | Cross-site scripting (XSS) in search | A03:2021 Injection | **Medium** |
| F6 | Unencrypted DNS and WPAD lookup | A05:2021 Security Misconfiguration | **Medium** |
| F7 | Security misconfiguration (permissive CORS, missing headers, information disclosure) | A05:2021 Security Misconfiguration | **Low** |
| F8 | Local SMB and IPv6 neighbour discovery traffic | Attack surface review | **Informational** |

## Methodology

1. **Reconnaissance:** Nmap, curl and Nikto to find the open port, HTTP headers and misconfigurations.
2. **Traffic interception:** Burp Suite Community as a proxy to inspect raw requests and responses.
3. **Manual validation:** each issue reproduced by hand; about 150 Nikto backup/cert hits were checked and discarded as false positives.
4. **Network analysis:** Wireshark captures of browsing, a failed login, a ping test and an Nmap SYN scan against my own loopback.
5. **Rating and reporting:** likelihood x impact, mapped to the OWASP Top 10, with remediation guidance.

## Repository Structure

```
README.md
report/
  Security-Assessment-Report.pdf
evidence/
  recon-01-nmap-service-scan.png
  recon-02-http-headers-and-nikto-start.png
  recon-03-nikto-results-a.png
  recon-04-nikto-results-b.png
  f1-sqli-01-login-payload.png
  f1-sqli-02-burp-capture-redacted.png
  f1-sqli-03-admin-login-confirmed.png
  f2-ftp-directory-exposure.png
  f3-cleartext-credentials-redacted.png
  f4-port-scan-pattern.png
  f5-xss-search-alert.png
  f6-dns-queries-redacted.png
  f8-protocol-hierarchy.png
```

## Tools Used

OWASP Juice Shop, Kali Linux, Docker, Nmap, Nikto, curl, Burp Suite Community, Firefox, Wireshark, Python 3 with Scapy.

## Data Handling

Passwords, session tokens, cookies, MAC addresses and personal IPv6 addresses were redacted from the screenshots before publishing. Raw packet captures are not published because they contain personal browsing traffic.

## Security and Ethical Use

This work was done for **educational and internship assessment purposes only**, against a training application I deployed myself. Never use these techniques against systems you do not own or have explicit written permission to test.

## Author

**Mubassir**
Security Intern, SWYNEX Technologies

**Program:** SWYNEX Technologies Internship | **Task:** 4, Security Assessment Report | **Repository:** GitHub
