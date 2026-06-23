# SAST Scan Report – OWASP Juice Shop

## Auditor Information

**Name:** Akash SP
**Assessment Type:** Static Application Security Testing (SAST)
**Target Application:** OWASP Juice Shop
**Assessment Date:** 22 June 2026

---

# 1. Executive Summary

A Static Application Security Testing (SAST) assessment was conducted against the OWASP Juice Shop source code using multiple automated security analysis tools.

The objective was to identify security vulnerabilities within the application's source code, validate findings, remove false positives, and provide remediation guidance.

Two SAST tools were utilized:

* Semgrep
* CodeQL

The assessment identified several security weaknesses including Injection flaws, exposed secrets, weak cryptographic practices, and Server-Side Request Forgery (SSRF) risks.

---

# 2. Scope

### Target

OWASP Juice Shop

### Assessment type

Static Application Security Testing (SAST)

### Source Code Language

* JavaScript
* TypeScript
* Node.js

### Analysis method

* Automated SAST scanning
* Finding validation
* False-positive triage
* CWE and OWASP Top 10 mapping

---

# 3. Tools used

| Tool                  | Purpose                                          |
| --------------------- | ------------------------------------------------ |
| Semgrep               | Static code analysis and security rule detection |
| CodeQL                | Advanced semantic code analysis                  |
| VS Code               | Source code review and validation                |
| Terminal / PowerShell | Scan execution and evidence collection           |

---

# 4. Methodology

The following methodology was used:

1. Clone and prepare the Juice Shop source code.
2. Execute Semgrep security scans.
3. Review and validate scanner findings.
4. Execute CodeQL database creation and analysis.
5. Review CodeQL findings.
6. Remove false-positive results.
7. Categorize findings using CWE and OWASP Top 10.
8. Document vulnerabilities and remediation guidance.

---

# 5. Findings summary

| ID   | Vulnerability                      | Severity | Tool    | CWE     |
| ---- | ---------------------------------- | -------- | ------- | ------- |
| F-01 | SQL Injection                      | High     | Semgrep | CWE-89  |
| F-02 | Hardcoded JWT Secret               | High     | Semgrep | CWE-798 |
| F-03 | Secret Exposure                    | Medium   | Semgrep | CWE-200 |
| F-04 | SQL Injection                      | High     | CodeQL  | CWE-89  |
| F-05 | Cross-Site Scripting (XSS)         | High     | CodeQL  | CWE-79  |
| F-06 | Server-Side Request Forgery (SSRF) | Medium   | CodeQL  | CWE-918 |
| F-07 | Weak Cryptographic Algorithm       | Medium   | CodeQL  | CWE-327 |

**Total Findings Identified:** 9

**False Positives Removed:** 2

**Confirmed Findings:** 7

---

# 6. Semgrep findings

## F-01: SQL Injection

### Severity

High

### CWE

CWE-89

### OWASP Mapping

A03:2021 – Injection

### Description

Semgrep detected SQL query construction patterns where untrusted user input may influence database queries.

### Impact

* Authentication bypass
* Unauthorized data access
* Data modification
* Data destruction

### Recommendation

* Use parameterized queries
* Use prepared statements
* Validate user input

---

## F-02: Hardcoded JWT Secret

### Severity

High

### CWE

CWE-798

### OWASP Mapping

A07:2021 – Identification and Authentication Failures

### Description

Semgrep identified JWT secrets embedded directly within application source code.

### Impact

* Token forgery
* Privilege escalation
* User impersonation

### Recommendation

* Store secrets in environment variables
* Use secret-management solutions
* Rotate exposed secrets

---

## F-03: Secret Exposure

### Severity

Medium

### CWE

CWE-200

### OWASP Mapping

A02:2021 – Cryptographic Failures

### Description

Sensitive information was identified within source code or configuration files.

### Impact

* Information disclosure
* Increased attack surface
* Unauthorized access risk

### Recommendation

* Remove secrets from repositories
* Store credentials securely
* Implement secret scanning

---

# 7. CodeQL findings

## F-04: SQL Injection

### Severity

High

### CWE

CWE-89

### OWASP Mapping

A03:2021 – Injection

### Description

CodeQL identified SQL injection patterns where user-controlled input could influence backend database operations.

### Recommendation

* Parameterized queries
* Prepared statements
* Input validation

---

## F-05: Cross-Site Scripting (XSS)

### Severity

High

### CWE

CWE-79

### OWASP Mapping

A03:2021 – Injection

### Description

CodeQL identified reflected and DOM-based XSS vectors where application input may be rendered without proper sanitization.

### Impact

* Session hijacking
* Credential theft
* Browser-based attacks

### Recommendation

* Context-aware output encoding
* Input sanitization
* Content Security Policy (CSP)

---

## F-06: Server-Side Request Forgery (SSRF)

### Severity

Medium

### CWE

CWE-918

### OWASP Mapping

A10:2021 – Server-Side Request Forgery

### Description

CodeQL identified functionality allowing user-supplied URLs to be processed by backend services.

### Impact

* Internal network access
* Cloud metadata exposure
* Information disclosure

### Recommendation

* Restrict outbound requests
* Use allowlists
* Validate URLs

---

## F-07: Weak Cryptographic Algorithm

### Severity

Medium

### CWE

CWE-327

### OWASP Mapping

A02:2021 – Cryptographic Failures

### Description

CodeQL detected usage patterns associated with outdated or weak cryptographic algorithms.

### Impact

* Reduced password security
* Increased brute-force susceptibility

### Recommendation

* Replace weak algorithms
* Use bcrypt, Argon2, or PBKDF2
* Follow modern cryptographic standards

---

# 8. False Positive validation

## Prototype Pollution

### Location

frontend/src/hacking-instructor/helpers/helpers.ts

### Result

The code traverses object properties but does not permit modification of:

* **proto**
* prototype
* constructor

### Decision

False Positive – Removed

---

## Explicit Unescape in Pug Template

### Location

views/promotionVideo.pug

### Result

The finding originated from a JavaScript inequality operator rather than unsafe Pug rendering syntax.

### Decision

False Positive – Removed

---

# 9. Evidence Collected

The following evidence was collected during the assessment:

* Semgrep execution screenshots
* Semgrep findings screenshots
* False-positive validation screenshots
* CodeQL database creation screenshots
* CodeQL query pack installation screenshots
* CodeQL query execution screenshots
* CodeQL findings screenshots
* SARIF output generation screenshots

---

# 10. Conclusion

The SAST assessment successfully identified multiple security vulnerabilities within the OWASP Juice Shop codebase.

The most critical issues involve:

1. SQL Injection
2. Cross-Site Scripting (XSS)
3. Hardcoded JWT Secrets

Additionally, CodeQL and Semgrep provided complementary coverage, improving overall visibility into application security weaknesses.

False-positive analysis reduced noise and improved result accuracy.

The assessment demonstrates the effectiveness of combining multiple SAST tools to identify security vulnerabilities during secure software development and review processes.
