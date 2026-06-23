# Application Security Assessment Report

## Target Application

OWASP Juice Shop

## Assessor

Akash SP

## Assessment Type

Application Security Assessment

## Assessment Date

 23 June 2026

---

# 1. Executive summary

An application security assessment was conducted on the OWASP Juice Shop application to identify security weaknesses across source code, application logic, and third-party dependencies.

The assessment consisted of:

* Manual Code Review
* Static Application Security Testing (SAST)
* Dependency and Supply Chain Review

Multiple security vulnerabilities were identified, including Injection flaws, insecure authentication practices, exposure of sensitive information, weak cryptographic implementations, and dependency-related risks.

The findings were categorized using CWE and OWASP Top 10 standards and prioritized according to potential business impact.

Overall Risk Rating: **High**

---

# 2. Scope & Methodology

## Scope

Target application:

OWASP Juice Shop

Technologies reviewed:

* Node.js
* JavaScript
* TypeScript
* Express Framework
* Third-party npm dependencies

---

## Methodology

The following methodology was applied:

### Manual code review

* Authentication logic review
* Input validation review
* Session management review
* Sensitive data handling review

### Static Application Security Testing

Tools used:

* Semgrep
* CodeQL

### Supply Chain Security Assessment

* Dependency inspection
* Package review
* Configuration review
* Secret exposure review

---

# 3. Manual code review findings

## M-01 Insecure JWT Secret Management

### Severity

High

### CWE

CWE-798

### Description

JWT secrets were exposed within application source code.

### Risk

Attackers may forge authentication tokens and impersonate users.

### Recommendation

Store secrets securely using environment variables or dedicated secret-management systems.

---

## M-02 Sensitive Information Exposure

### Severity

Medium

### CWE

CWE-200

### Description

Sensitive information was identified within source code and configuration resources.

### Recommendation

Remove secrets from source repositories and rotate exposed credentials.

---

# 4. SAST Results

| ID   | Finding                            | Severity | Tool    |
| ---- | ---------------------------------- | -------- | ------- |
| F-01 | SQL Injection                      | High     | Semgrep |
| F-02 | Hardcoded JWT Secret               | High     | Semgrep |
| F-03 | Secret Exposure                    | Medium   | Semgrep |
| F-04 | SQL Injection                      | High     | CodeQL  |
| F-05 | Cross-Site Scripting (XSS)         | High     | CodeQL  |
| F-06 | Server-Side Request Forgery (SSRF) | Medium   | CodeQL  |
| F-07 | Weak Cryptographic Algorithm       | Medium   | CodeQL  |

---

## Key SAST Findings

### SQL Injection

**Severity:** High

**CWE:** CWE-89

Improper handling of user-controlled input may allow database manipulation.

---

### Cross-Site Scripting (XSS)

**Severity:** High

**CWE:** CWE-79

Unsanitized input may allow execution of malicious scripts in users' browsers.

---

### Server-Side Request Forgery (SSRF)

**Severity:** Medium

**CWE:** CWE-918

Backend services may access attacker-controlled URLs.

---

### Weak Cryptography

**Severity:** Medium

**CWE:** CWE-327

Weak hashing mechanisms may expose sensitive information.

---

# 5. Supply Chain & Dependency Risks

## Observations

Dependency review identified several security considerations:

### Third-Party Dependency Risk

The application relies on numerous external npm packages.

Risks include:

* Vulnerable dependencies
* Malicious package updates
* Dependency confusion attacks
* Supply chain compromise

---

### Secret Exposure Risk

Sensitive configuration values should not be committed to repositories.

---

### Outdated Package Risk

Outdated dependencies may contain publicly known vulnerabilities.

---

## Recommendations

* Regularly update dependencies
* Use automated dependency scanning
* Enable Dependabot or similar tooling
* Review third-party packages before adoption
* Implement Software Composition Analysis (SCA)

---

# 6. Risk Rating Summary

| Severity | Count |
| -------- | ----- |
| High     | 4     |
| Medium   | 3     |
| Low      | 0     |

---

## Overall risk

**High**

The presence of Injection vulnerabilities, authentication weaknesses, and exposed secrets creates significant security risk requiring remediation.

---

# 7. Remediation recommendations

## SQL Injection

* Use parameterized queries
* Use prepared statements
* Validate all user input

---

## Cross-Site Scripting

* Sanitize user input
* Encode output
* Deploy Content Security Policy (CSP)

---

## JWT Secret Exposure

* Store secrets in environment variables
* Rotate exposed credentials
* Use secret-management solutions

---

## SSRF

* Restrict outbound connections
* Validate URLs
* Implement allowlists

---

## Weak Cryptography

* Replace weak algorithms
* Use bcrypt or Argon2
* Follow current cryptographic standards

---

## Dependency risks

* Perform regular dependency audits
* Patch vulnerable packages
* Use automated monitoring solutions

---

# 8. Prioritized action plan

| Priority | Action                                     |
| -------- | ------------------------------------------ |
| P1       | Fix SQL Injection vulnerabilities          |
| P1       | Remove hardcoded JWT secrets               |
| P1       | Address Cross-Site Scripting findings      |
| P2       | Implement secure cryptographic algorithms  |
| P2       | Restrict SSRF attack paths                 |
| P3       | Review and update third-party dependencies |
| P3       | Implement continuous security scanning     |

---

# Conclusion

The assessment identified multiple security weaknesses affecting application security, authentication, data protection, and dependency management.

The highest-risk findings involve Injection vulnerabilities and exposed authentication secrets. Immediate remediation of High severity findings is recommended.

Combining Manual Code Review, SAST analysis, and Supply Chain assessment provided broader visibility into the application's security posture and helped identify risks that may not be visible through a single testing approach.
