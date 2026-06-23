# Supply Chain Security Report

## Project information

- Project: OWASP Juice Shop
- Tool Used: CycloneDX
- Vulnerability Scanner: Snyk CLI
- Date: 19-06-2026

---

## SBOM generation

An SBOM was generated using CycloneDX.

Output file:

- bom.json

Purpose:

- Inventory software dependencies
- Identify third-party packages
- Support vulnerability management
- Improve software supply chain visibility

---

## Vulnerability scan results

The project dependencies were scanned using Snyk CLI.

### Critical vulnerabilities

- Uncaught Exception (multer)

### High severity vulnerabilities

- Authentication Bypass
- Code Injection
- Prototype Pollution
- Directory Traversal
- Denial of Service
- Weak Cryptographic Hash Usage
- Resource Allocation Without Limits

### Medium severity vulnerabilities

- Cross-Site Scripting (XSS)
- Regular Expression Denial of Service (ReDoS)
- Improper Authentication
- Improper Validation
- Resource Exhaustion
- Prototype Pollution
- Information Exposure

---

## Supply Chain risks identified

1. Outdated dependencies

Several dependencies are outdated and contain publicly known vulnerabilities.

2. Vulnerable third-party Packages

Multiple packages contain critical and high severity security flaws.

3. Dependency Chain risk

Vulnerabilities were inherited through nested dependencies.

4. Authentication and Authorization weaknesses

Several packages contain authentication bypass vulnerabilities.

5. Injection risks

Code injection and XSS vulnerabilities were detected.

---

## Recommendations

1. Upgrade vulnerable packages to recommended versions.
2. Remove unused dependencies.
3. Continuously monitor dependencies using Snyk.
4. Regenerate SBOM after dependency updates.
5. Integrate dependency scanning into CI/CD pipelines.
6. Review third-party package trustworthiness before adoption.

---

## Conclusion

The OWASP Juice Shop application contains numerous vulnerable dependencies, including Critical, High, and Medium severity findings. The generated SBOM and Snyk analysis provide visibility into supply chain risks and help prioritize remediation efforts.