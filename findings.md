# Findings

This document summarizes the confirmed vulnerabilities identified during the security assessment of OWASP Juice Shop.

---

## 🔴 Critical: SQL Injection – Authentication Bypass
**Endpoint:** `/rest/user/login`  
**Impact:** Full login bypass without credentials  
**Payload Example:** `' OR 1=1--`  
**Severity:** 9.8 (Critical)  
**OWASP Mapping:** A03 – Injection

The login function fails to sanitize SQL injection payloads, allowing attackers to authenticate without a valid password.

---

## 🔴 High: Broken Access Control – Admin API Exposure
**Endpoint:** `/rest/admin/application-version`  
**Impact:** Unauthorized access to admin configuration  
**Severity:** 8.7 (High)  
**OWASP Mapping:** A01 – Broken Access Control

Normal users can access admin-only API endpoints without authentication or role validation.

---

## 🔴 High: Sensitive Data Exposure / Insecure API
**Endpoint:** `/api/Feedbacks/`  
**Impact:** User IDs, masked emails, comments, ratings leaked  
**Severity:** 7.4 (High)  
**OWASP Mapping:** A02 – Cryptographic Failures

The API exposes user feedback data without authentication or data minimization.

---

## 🟠 Medium: Reflected Cross-Site Scripting (XSS)
**Endpoint:** `/#/search?q=`  
**Payload:** `'><img src=x onerror=alert('XSS')>`  
**Severity:** 6.1 (Medium)  
**OWASP Mapping:** A03 – Injection

Unsanitized search parameter allows JavaScript execution.

---

## 🟡 Medium: Weak Authentication / Brute Force
**Endpoint:** `/rest/user/login`  
**Impact:** Weak passwords accepted, no brute-force protection  
**Severity:** 7.5 (High)  
**OWASP Mapping:** A07 – Identification & Authentication Failures

The login system accepts commonly used passwords (e.g., `admin123`) and lacks rate limiting.

---

## Summary Table

| Vulnerability | Severity | OWASP Top 10 | Confirmed |
|--------------|----------|--------------|-----------|
| SQL Injection | Critical | A03 | ✔ |
| Broken Access Control | High | A01 | ✔ |
| Sensitive Data Exposure | High | A02 | ✔ |
| XSS | Medium | A03 | ✔ |
| Weak Authentication | Medium/High | A07 | ✔ |

---

## Conclusion

These vulnerabilities significantly compromise the confidentiality, integrity, and availability of the application. Remediation should begin with SQL Injection and Broken Access Control due to their severe impact.
