# ArcByte Application Security Assessment Project

## Overview

This repository contains the deliverables completed as part of the ArcByte Cybersecurity Internship Application Security Assessment project.

The objective of this project was to perform a comprehensive security assessment of the OWASP Juice Shop application using multiple security testing methodologies, including:

- Manual Code Review
- Static Application Security Testing (SAST)
- Supply Chain Security Review
- Vulnerability Analysis and Risk Assessment
- Security Reporting and Remediation Recommendations

The assessment findings were documented using industry-recognized standards such as:

- OWASP Top 10 (2021)
- Common Weakness Enumeration (CWE)
- Secure Software Development Practices

---

## Assessment scope

Target application:

**OWASP Juice Shop**

Technology Stack Reviewed:

- JavaScript
- TypeScript
- Node.js
- Express Framework
- npm Dependencies

---

## Project deliverables

### Security reports

- Application Security Assessment Report
- Manual Code Review Report
- SAST Scan Report
- Supply Chain Security Report

### Supporting evidence

- Semgrep Scan Results
- CodeQL Scan Results
- Manual Review Screenshots
- Supporting Documentation

---

## Security activities performed

### Manual code review

Performed source-code inspection to identify:

- Authentication weaknesses
- Sensitive information exposure
- Input validation issues
- Secure coding violations

### Static Application Security Testing (SAST)

Tools used:

- Semgrep
- CodeQL

Findings included:

- SQL Injection
- Cross-Site Scripting (XSS)
- Hardcoded Secrets
- Server-Side Request Forgery (SSRF)
- Weak Cryptographic Practices

### Supply Chain assessment

Reviewed:

- Third-party dependencies
- Dependency risks
- Potential supply chain attack vectors
- Security update considerations

---

## Environment and Execution Notes

During the assessment period, the ArcForge cloud workspace experienced service interruptions and accessibility issues that prevented portions of the assessment from being completed within the hosted environment.

To ensure project completion and continue security testing activities, assessment tasks were performed using a personal local environment configured to mirror the required tooling and workflow.

Tools installed locally included:

- Visual Studio Code
- Semgrep
- CodeQL
- Git
- PowerShell

All findings, reports, and screenshots contained in this repository were generated through legitimate security assessment activities conducted on the project scope provided for the internship.

---

## Key Outcomes

The assessment identified multiple security issues across the application, including:

- Injection vulnerabilities
- Authentication weaknesses
- Sensitive information exposure
- Weak cryptographic implementations
- Dependency-related risks

Each finding was documented with:

- Severity Rating
- CWE Mapping
- OWASP Classification
- Risk Description
- Remediation Guidance

---

## Author

**Akash SP**

Cybersecurity Student | BCA Cybersecurity

ArcByte Internship Project – 2026

---

## Disclaimer

This repository was created solely for educational, internship, and security assessment purposes.

OWASP Juice Shop is an intentionally vulnerable application designed for security training and learning.