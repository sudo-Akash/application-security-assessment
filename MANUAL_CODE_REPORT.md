# OWASP Juice Shop Security Assessment Report

## Student Details

* **Name:** Akash SP
* **Assessment:** Static Application Security Review
* **Application:** OWASP Juice Shop
* **Date:**  17 June 2026

---

# Introduction

This report presents the results of a static security assessment performed on the OWASP Juice Shop application. The objective of the assessment was to identify security vulnerabilities by reviewing the application's source code and evaluating insecure coding practices. Four significant vulnerabilities were identified during the review, namely XML External Entity (XXE), Cross-Site Request Forgery (CSRF), Insecure Direct Object Reference (IDOR), and Server-Side Code Injection through the use of the `eval()` function.

---

# Vulnerability 1: XML External Entity (XXE)

## Vulnerability type

XML External Entity (XXE)

## Severity

High

## Affected file

`routes/fileUpload.ts`

## Description

XML External Entity (XXE) attacks occur when an application processes XML input containing external entity references. If external entities are enabled, attackers can manipulate XML documents to access local files, internal services, and sensitive server resources.

The file upload functionality processes XML-based content without sufficient protection against malicious entity declarations, making the application vulnerable to XXE attacks.

## Impact

An attacker could:

* Read sensitive files from the server.
* Access internal network services.
* Retrieve configuration files and credentials.
* Perform Server-Side Request Forgery (SSRF).
* Leak confidential system information.


## Risk assessment

Because XXE can expose critical system files and internal infrastructure, it is considered a High severity vulnerability.

## Recommended remediation

* Disable external entity processing in XML parsers.
* Use secure XML libraries.
* Validate uploaded XML documents.
* Reject files containing external entity declarations.

---

# Vulnerability 2: Cross-Site Request Forgery (CSRF)

## Vulnerability Type

Cross-Site Request Forgery (CSRF)

## Severity

Medium

## Affected File

`routes/updateUserProfile.ts`

## Description

Cross-Site Request Forgery (CSRF) occurs when an attacker tricks an authenticated user into performing actions they did not intend. The application updates user profiles without implementing proper anti-CSRF tokens.

Instead, the application relies on checking the Origin and Referer headers, which is not considered a reliable defense mechanism.

## Code snippet

```typescript
challengeUtils.solveIf(challenges.csrfChallenge, () => {
  return (
    (req.headers.origin?.includes('://htmledit.squarefree.com')) ??
    (req.headers.referer?.includes('://htmledit.squarefree.com'))
  ) && req.body.username !== user.username
})
```

## Impact

An attacker could:

* Change user profile information.
* Modify account settings.
* Perform unauthorized actions on behalf of users.
* Abuse active authenticated sessions.


## Risk Assessment

The lack of proper CSRF protection may allow unauthorized state-changing actions, making this a Medium severity vulnerability.

## Recommended Remediation

* Implement anti-CSRF tokens.
* Use SameSite cookie protections.
* Validate all state-changing requests.
* Avoid relying solely on Origin and Referer headers.

---

# Vulnerability 3: Insecure Direct Object Reference (IDOR)

## Vulnerability type

Insecure Direct Object Reference (IDOR)

## Severity

Medium to high

## Affected file

`routes/basket.ts`

## Description

An Insecure Direct Object Reference (IDOR) vulnerability occurs when user-supplied identifiers are used to access resources without proper authorization checks.

The application retrieves basket information directly from a user-controlled identifier without verifying ownership of the requested basket.

## Code snippet

```typescript
const id = req.params.id

const basket = await BasketModel.findOne({
  where: { id }
})
```

## Impact

An attacker could:

* Access shopping baskets belonging to other users.
* View sensitive customer information.
* Enumerate application data.
* Bypass authorization mechanisms.


## Risk Assessment

Improper authorization checks can lead to unauthorized access to user data, making this a Medium-High severity vulnerability.

## Recommended remediation

* Verify resource ownership before access.
* Implement server side authorization checks.
* Restrict access to authenticated owners only.
* Use indirect references where possible.

---

# Vulnerability 4: Server-Side Code Injection via eval()

## Vulnerability type

Server-Side Code Injection / Server-Side Template Injection (SSTI)

## Severity

High

## Affected file

`routes/userProfile.ts`

## Description

The application extracts user-controlled content and executes it using JavaScript's `eval()` function. The `eval()` function executes strings as code, making it extremely dangerous when user input is involved.

An attacker may inject malicious code that gets executed on the server.

## Code snippet

```typescript
const code = username?.substring(2, username.length - 1)

username = eval(code)
```

## Impact

An attacker could:

* Execute arbitrary code on the server.
* Access sensitive application data.
* Modify application behavior.
* Potentially achieve Remote Code Execution (RCE).


## Risk assessment

Executing user-controlled input through `eval()` is a critical security weakness that may lead to complete compromise of the application.

## Recommended remediation

* Remove all usage of `eval()`.
* Treat all user input as untrusted.
* Use safe parsing mechanisms.
* Apply strict input validation and output encoding.

---

# Conclusion

The static security assessment identified four major vulnerabilities within the OWASP Juice Shop application.

| Vulnerability                           | Severity    |
| --------------------------------------- | ----------- |
| XML External Entity (XXE)               | High        |
| Cross-Site Request Forgery (CSRF)       | Medium      |
| Insecure Direct Object Reference (IDOR) | Medium-High |
| Server-Side Code Injection (eval)       | High        |

Among the identified vulnerabilities, the XXE vulnerability and the use of `eval()` represent the highest risks due to their potential impact on confidentiality, integrity, and availability of the system.

Immediate remediation of these vulnerabilities is recommended to improve the overall security posture of the application.

---

# References

1. OWASP Top 10
2. OWASP Juice Shop Documentation
3. OWASP Testing Guide
4. OWASP Cheat Sheet Series
