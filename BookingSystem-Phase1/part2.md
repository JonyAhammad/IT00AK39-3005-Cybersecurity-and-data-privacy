
# 1️⃣ Introduction for part 2

**Tester(s):**  
- Name:  Jony Ahammad and rex

**Purpose:** 
# Purpose of the Test

The purpose of this test is to **assess the security and privacy of the user registration functionality** in the system. Specifically, it aims to:

1. **Identify vulnerabilities in registration and authentication flows**  
   - Detect flaws that could allow unauthorized account creation, privilege escalation, or bypassing authentication.  
   - Ensure that user roles (reservist vs. administrator) are correctly assigned and cannot be manipulated.  

2. **Evaluate input validation and injection risks**  
   - Test for SQL injection, cross-site scripting (XSS), or other malicious input that could compromise the system.  

3. **Verify session management and data protection**  
   - Ensure sessions are secure, expire appropriately, and cannot be hijacked.  
   - Confirm sensitive user data is encrypted in transit and at rest.  

4. **Check error handling and information leakage**  
   - Ensure error messages do not expose system details or personal data.  

5. **Assess GDPR compliance and Privacy by Design adherence**  
   - Confirm that only necessary personal data is collected and anonymized when possible.  
   - Verify that privacy is embedded in the system by default and that users’ rights (deletion, correction, data portability) are supported.  

6. **Use automated tools (like OWASP ZAP) to identify security weaknesses**  
   - Scan the registration process for common web application vulnerabilities and anomalies.  

**Overall**, the goal is to detect anomalies and security weaknesses that could be exploited by attackers while ensuring that the system protects user data and aligns with GDPR and Privacy by Design principles.



**Scope:**  
# Scope

- **Tested components:** User registration page, input fields, validation, basic authentication flow.  
- **Exclusions:** Full admin features, resource booking, session management, and other phases not related to registration.  
- **Test approach:** Gray-box testing.
---

**Test environment & dates:**  
- Start: 23-11.2025  
- End: 28-11-2025
- Test environment details (OS, runtime, DB, browsers):

**Assumptions & constraints:**  

- Credentials for reservist and admin provided.  
- Limited time for testing.  
- Only registration functionality is in scope.  
- Testing done in a safe environment, not affecting production.  
- Gray-box approach with partial system knowledge.  
- Using tools like OWASP ZAP for scanning.  
- Must follow GDPR and Privacy by Design rules.

- 

---
**1.docker setup and run compose yml file**
---

<img width="2517" height="1326" alt="image" src="https://github.com/user-attachments/assets/42b2e4f2-ca32-479c-bd7c-683c3533420c" />


**2.docker setup and run the compose yml file in browser**
---

<img width="1684" height="991" alt="image" src="https://github.com/user-attachments/assets/0fed7762-7dba-4eb4-91d1-c0fe83de77d1" />


**3.Exploring the database schema and viewing user data**
---
<img width="1105" height="621" alt="image" src="https://github.com/user-attachments/assets/034b62a3-bca2-4177-a317-086880a323d6" />
---
<img width="1504" height="560" alt="image" src="https://github.com/user-attachments/assets/373d52ed-d789-4a53-8af3-90c796fb8273" />









# 2️⃣ Executive Summary

**Short summary (1-2 sentences):**  
The system contains several security weaknesses that increase the risk of client-side attacks, sensitive information exposure, and unauthorized request execution. Immediate remediation is required to reduce the attack surface and protect users

**Overall risk level:** (Low / Medium / High / Critical)

**Top  immediate actions:**  

1.  Absence of Anti-CSRF Tokens -  Medium


---

# 3️⃣ Severity scale & definitions

|  **Severity Level**  | **Description**                                                                                                              | **Recommended Action**           |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
|      🔴 **High**     | A serious vulnerability that can lead to full system compromise or data breach (e.g., SQL Injection, Remote Code Execution). | *Immediate fix required*         |
|     🟠 **Medium**    | A significant issue that may require specific conditions or user interaction (e.g., XSS, CSRF).                              | *Fix ASAP*                       |
|      🟡 **Low**      | A minor issue or configuration weakness (e.g., server version disclosure).                                                   | *Fix soon*                       |
| 🔵 **Info** | No direct risk, but useful for system hardening (e.g., missing security headers).                                            | *Monitor and fix in maintenance* |


---

# 4️⃣ Findings (filled with examples → replace)

> Fill in one row per finding. Focus on clarity and the most important issues.

| ID | Severity | Finding | Description | Evidence / Proof |
|------|-----------|----------|--------------|------------------|
| F-01 | 🔴 High | SQL Injection in registration | Input field allows `' OR '1'='1` injection | Screenshot or sqlmap result |
| F-02 | 🟠 Medium | Session fixation | Session ID remains unchanged after login | Burp log or response headers |
| F-03 | 🟡 Low | Weak password policy | Accepts passwords like "12345" | Screenshot of registration success |

---

> [!NOTE]
> Include up to 5 findings total.   
> Keep each description short and clear.

---

# 5️⃣ OWASP ZAP Test Report (Attachment)

[ZAP Report](ZAP-REPORT-PART-2.MD)
---


**Purpose:**  
- Attach or link your OWASP ZAP scan results.
- http://localhost:8000/

  <img width="948" height="1349" alt="image" src="https://github.com/user-attachments/assets/414afd34-eca3-439f-857e-5bf66ffe91d1" />


---
**zap screen**
---
<img width="1436" height="1236" alt="image" src="https://github.com/user-attachments/assets/73804dce-f002-42f3-ac9b-f9cd8227cebf" />
---
<img width="1431" height="1352" alt="image" src="https://github.com/user-attachments/assets/4fd66fb9-38ff-47ec-bca0-1a3a4fdc073d" />




**ZAP testing**
---
<img width="1427" height="1347" alt="image" src="https://github.com/user-attachments/assets/7d34f86a-3915-489a-889c-7deb371d8ea2" />




**Instructions (CMD version):**
1. Run OWASP ZAP baseline scan:  
   ```bash
   zap-baseline.py -t https://example.com -r zap_report_round1.html -J zap_report.json
   ```
2. Export results to markdown:  
   ```bash
   zap-cli report -o zap_report_round1.md -f markdown
   ```
3. Save the report as `zap_report_round1.md` and link it below.

---
> [!NOTE]
> 📁 **Attach full report:** → `check itslearning` → **Add a link here**

---
