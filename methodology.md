# Methodology

This security assessment followed a structured, industry-standard approach based on the **OWASP Web Security Testing Guide (WSTG)**.  
The assessment targeted the locally hosted OWASP Juice Shop instance at `http://localhost:3000`.

---

## 1. Testing Approach

The methodology included:

### ✔ Black-box penetration testing  
The tester had no internal access to the application’s source code or server.

### ✔ Manual Testing  
Hands-on exploitation attempts were performed for:
- Authentication
- Session management
- Authorization
- Input validation
- Error handling
- API security

### ✔ Tool-Assisted Testing  
Tools were used only to assist manual findings (not fully automated):

- Burp Suite Community Edition  
- OWASP ZAP  
- Browser DevTools  
- Docker (for application hosting)

---

## 2. Phases of Testing

### **Phase 1: Reconnaissance**
- Identified exposed endpoints through Burp Suite HTTP history  
- Mapped API structure (`/api/*` and `/rest/*` routes)  
- Observed login flow, session tokens, and JWT structure  

### **Phase 2: Vulnerability Discovery**
Performed tests from the OWASP Top 10:

- Injection testing (SQLi payloads)
- Authentication testing (weak passwords, brute force)
- Access control testing (admin endpoints, IDOR)
- XSS testing (URL parameters, search bar, stored inputs)
- Sensitive data exposure through APIs

### **Phase 3: Exploitation**
Confirmed vulnerabilities by:
- Bypassing login with SQL injection  
- Logging in using weak passwords  
- Executing JavaScript in user sessions  
- Accessing admin-only API endpoints  
- Retrieving sensitive user feedback data

### **Phase 4: Documentation**
Each vulnerability was documented with:
- Description  
- Steps to reproduce  
- Tools used  
- Payloads  
- Impact  
- Severity (CVSS 3.1)  
- Remediation steps  

---

## 3. Standards Followed

- **OWASP Top 10 – 2021**
- **OWASP ASVS (Application Security Verification Standard)**
- **OWASP WSTG (Web Security Testing Guide)**  
- **CVSS 3.1 Scoring System**

---

## 4. Limitations

- Testing was limited to the local environment  
- Only manual review (no authenticated API fuzzing)  
- Source code was not reviewed (black-box testing)

---

## 5. Conclusion

The methodology revealed multiple critical vulnerabilities, including SQL Injection, Broken Access Control, and Sensitive Data Exposure.  
These findings indicate severe weaknesses in input validation, access control, and data handling.
