
# 1️⃣ Introduction

**Tester(s):**  
- Name:  Jony Ahammad and rex

**Purpose:**  
- Describe the purpose of this test (e.g., identify vulnerabilities in registration and authentication flows).

**Scope:**  
- Tested components:  
- Exclusions:  
- Test approach: Gray-box / Black-box / White-box

**Test environment & dates:**  
- Start: 23-11.2025  
- End:  
- Test environment details (OS, runtime, DB, browsers):

**Assumptions & constraints:**  
- e.g., credentials provided, limited time, etc.

---
**1.docker setup and run compose yml file**
---

<img width="2502" height="1325" alt="image" src="https://github.com/user-attachments/assets/9b7e51b9-4f4f-4425-9496-aafff7fd2838" />

**2.docker setup and run the compose yml file in browser**
---
<img width="1832" height="1041" alt="image" src="https://github.com/user-attachments/assets/c5bf7a5b-b3b4-4975-b32c-6df1959d6eee" />

**3.Exploring the database schema and viewing user data**
---
<img width="1101" height="552" alt="image" src="https://github.com/user-attachments/assets/af19f8bf-fb80-4fae-a05c-3a5edd214ddd" />






# 2️⃣ Executive Summary

**Short summary (1-2 sentences):**  
The system contains several security weaknesses that increase the risk of client-side attacks, sensitive information exposure, and unauthorized request execution. Immediate remediation is required to reduce the attack surface and protect users

**Overall risk level:** (Low / Medium / High / Critical)

**Top 5 immediate actions:**  
1.  Content Security Policy (CSP) Header Not Set -  Medium
2.  SQL Injection -  high
3.  Application Error Disclosure -  Medium
4.  Absence of Anti-CSRF Tokens -  Medium
5.  Path Traversal-  low

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

BookingSystem-Phase1/ZAP-Report.md

**Purpose:**  
- Attach or link your OWASP ZAP scan results.
- http://localhost:8000/

  <img width="948" height="1349" alt="image" src="https://github.com/user-attachments/assets/414afd34-eca3-439f-857e-5bf66ffe91d1" />


---
<img width="1502" height="1368" alt="image" src="https://github.com/user-attachments/assets/f88eb137-f480-40d4-85a7-6c5479de3191" />
---

<img width="1261" height="1307" alt="image" src="https://github.com/user-attachments/assets/616e0eee-6b59-4a75-b392-e19076a3e5d9" />



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
