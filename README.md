# Owasp-Juice-Shop---VAPT
VAPT report on OWASP Juice Shop Covering Owasp Top 10 : 2025 Vulnerabilities

# OWASP Juice Shop — Web Application VAPT Report

A hands-on Vulnerability Assessment and Penetration Testing (VAPT) project performed against **[OWASP Juice Shop](https://owasp-juice.shop/)**, an intentionally vulnerable web application maintained by OWASP for security training. This repository contains the full assessment report, all supporting evidence, and a summary of the five vulnerabilities identified, each mapped to the **OWASP Top 10:2025** and relevant CWEs.

> ⚠️ **Disclaimer:** All testing was performed exclusively against OWASP Juice Shop — a deliberately vulnerable application built for this purpose — either on a local Docker instance or the official public demo (`https://juice-shop.herokuapp.com`). No other system was tested. This project is for educational and skill-demonstration purposes only.

---

## 📄 Report

| Format | File |
|---|---|
| PDF | [`Vulnerability_Assessment_Report.pdf`](./Vulnerability_Assessment_Report.pdf) |
| Word (.docx) | [`Vulnerability_Assessment_Report.docx`](./Vulnerability_Assessment_Report.docx) |

---

## 🎯 Scope

| | |
|---|---|
| **Target Application** | OWASP Juice Shop |
| **Target URL** | `https://juice-shop.herokuapp.com` (public demo) / `http://localhost:3000` (local Docker instance) |
| **Testing Tools** | Burp Suite (Proxy, Repeater), Firefox DevTools, Docker |
| **Testing Environment** | Kali Linux (VirtualBox VM) |
| **Tested By** | Asha P S |

---

## 🔍 Findings Summary

| # | Vulnerability | OWASP Top 10:2025 | CWE | Risk |
|---|---|---|---|---|
| 4.1 | SQL Injection (SQLi) — Authentication Bypass | A05 – Injection | CWE-89 | **Critical** |
| 4.2 | Cross-Site Scripting (XSS) — DOM-based Search Payload Execution | A05 – Injection | CWE-79 | **High** |
| 4.3 | Insecure Direct Object Reference (IDOR) — Basket Access | A01 – Broken Access Control | CWE-639 | **High** |
| 4.4 | Broken Authentication — Weak Administrator Credentials | A07 – Authentication Failures | CWE-287, CWE-521 | **High** |
| 4.5 | Security Misconfiguration — Exposed Directory Listing & Stack Trace Disclosure | A02 – Security Misconfiguration | CWE-548, CWE-209 | **Medium** |

Each finding in the report includes: Description, Objective, Testing Environment, step-by-step Test Procedure, Observation, Root Cause, Evidence (screenshots), Impact, Recommendation, and References.

---

## 🧪 Highlights

- **4.1 SQLi** — Bypassed admin login using `' OR 1=1--` with no valid credentials; also found a second, independent error-based SQL Injection point in the product search endpoint via Burp Suite, which leaked the raw database query.
- **4.2 XSS** — Achieved DOM-based XSS using `<iframe src="javascript:alert('XSS')">` in the search bar; confirmed on both the local instance and the live public target.
- **4.3 IDOR** — Used Burp Repeater to swap a basket ID in an otherwise-valid, authenticated request and retrieved another user's basket contents — confirmed independently by the application's own challenge tracker.
- **4.4 Broken Authentication** — Logged in as administrator using a commonly-guessed weak password (`admin123`), with no account lockout or rate-limiting in place.
- **4.5 Security Misconfiguration** — Discovered an exposed `/ftp/` directory listing containing a password database (`.kdbx`) and backup files, plus a stack trace leak revealing internal server file paths.

---

## 📂 Repository Structure

```
.
├── README.md
├── Vulnerability_Assessment_Report.pdf
├── Vulnerability_Assessment_Report.docx
└── screenshots/
    ├── 4.1-SQL-Injection/
    ├── 4.2-XSS/
    ├── 4.3-IDOR/
    ├── 4.4-Broken-Authentication/
    └── 4.5-Security-Misconfiguration/
```

---

## 🛠️ Tools & Environment

- **OWASP Juice Shop** — [github.com/juice-shop/juice-shop](https://github.com/juice-shop/juice-shop)
- **Burp Suite** — Proxy, Repeater
- **Docker** — for running a local instance of Juice Shop
- **Kali Linux** (VirtualBox VM)
- **Firefox DevTools** — for request inspection and token handling

---

## 📚 References

- [OWASP Top 10:2025](https://owasp.org/Top10/)
- [OWASP Juice Shop Official Site](https://owasp-juice.shop/)
- [PortSwigger Web Security Academy](https://portswigger.net/web-security)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)

---

## 👤 Author

**Asha P S**
Security Testing / VAPT Internship Project!
