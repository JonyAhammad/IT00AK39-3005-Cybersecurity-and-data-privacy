# 1️⃣ Phase 2 – Test Report

## **Tester(s)**
- **Jony Ahammad**
- **Rex**

---

## **Purpose of the Test**

The purpose of this Phase 2 test is to evaluate the **security, functionality, and privacy protections** of the updated Booking System application. Since Phase 2 improves password handling and backend logic, this test ensures that the new changes do not introduce vulnerabilities and that the system aligns with GDPR and Privacy-by-Design requirements.

### **Key Testing Objectives**

### **1. Identify vulnerabilities in registration and authentication flows**
- Check for unauthorized account creation.
- Ensure user roles (reservist vs. admin) cannot be changed or manipulated through form tampering or API calls.
- Verify that authentication cannot be bypassed.

### **2. Evaluate input validation and injection risks**
- Test registration form with SQL injection payloads.
- Test for cross-site scripting (XSS) via input fields.
- Confirm that invalid or malicious data is blocked.

### **3. Verify session management and data protection**
- Confirm that session cookies are handled securely.
- Ensure sessions expire correctly after logout.
- Check whether personal data is safely handled.

### **4. Check error handling and information leakage**
- Ensure errors do not reveal internal system details.
- Confirm that messages do not expose whether an email address exists.

### **5. Assess GDPR compliance and Privacy by Design**
- Verify minimal data collection during registration.
- Assess whether the system supports user rights (e.g., deletion, correction).
- Check whether sensitive data appears encrypted or protected.

### **6. Use automated tools to detect vulnerabilities**
- OWASP ZAP scans were used (Spider + Active Scan).
- Alerts were reviewed and compared to previous phases.

> **Overall Goal:**  
To identify weaknesses in the registration and authentication logic, evaluate improvements in Phase 2, and ensure the system protects user data according to GDPR.

---

## **Scope**

### ✔️ **Tested Components**
- Registration page  
- Registration validation  
- Authentication (login/logout)  
- Backend registration logic  
- Database interaction for user creation  
- OWASP ZAP scan on registration and login endpoints  

### ❌ **Excluded Components**
- Full administrator dashboard  
- Resource booking system  
- Reservation modification/deletion  
- Admin-level user controls  
- Email verification or password reset features  

### **Test Approach: Gray-box**
- Partial knowledge of system behavior  
- No access to source code  
- Manual testing + automated scanning  

---

## **Test Environment & Dates**

### **Test Period**
- **Start date:** 6.12.2025  
- **End date:** 8.12.2025  

### **Environment Details**
- **Operating System:** Windows 10  
- **Runtime:** Docker Desktop  
- **Deployment:**  
  - `docker compose up -d` from the Phase 2 project folder  
- **Containers Used:**  
  - `cybersec-web-phase2` – web application  
  - `cybersec-db-phase2` – PostgreSQL database  
- **Browsers Used:**  
  - Google Chrome (latest)  
  - Mozilla Firefox (latest)  
- **Tools Used:**  
  - OWASP ZAP  
  - Postman (for verifying API behavior)

---

## **Assumptions & Constraints**

- Valid credentials for both **reservist** and **administrator** were provided for login tests.  
- Only **registration and authentication** are in scope for Phase 2 test reporting.  
- Testing time was limited, so deeper admin features were not analyzed.  
- All testing was done locally using **Docker Desktop**, not a production environment.  
- Some behaviors were inferred from system responses, as server logs were not accessible.  
- OWASP ZAP was used responsibly to avoid overloading the application.  
- GDPR and Privacy-by-Design guidelines were followed when handling test data.

---



- 

---
**1.docker setup and run compose yml file**
---

<img width="2500" height="1301" alt="image" src="https://github.com/user-attachments/assets/1ac93c0d-4c7e-445c-ae49-21745585e00d" />
---
**1.docker setup for all file**
---
<img width="2221" height="1204" alt="image" src="https://github.com/user-attachments/assets/8611f203-7157-4559-bfb0-6779f1acd626" />
---
**All services (in current project folder):**
---

PS C:\Users\mdjon\desktop\docker3\phase2> docker compose ls
NAME                    STATUS              CONFIG FILES
cybersec-phase1-part1   running(2)          C:\Users\mdjon\Desktop\Docker\phase1\part1\docker-compose.yml
cybersec-phase1-part2   running(2)          C:\Users\mdjon\desktop\docker2\phase1\part2\docker-compose.yml
cybersec-phase2         running(2)          C:\Users\mdjon\desktop\docker3\phase2\docker-compose.yml
PS C:\Users\mdjon\desktop\docker3\phase2> docker compose logs -f
cybersec-web-phase2  | Watcher Process started.
cybersec-db-phase2   | The files belonging to this database system will be owned by user "postgres".
cybersec-db-phase2   | This user must also own the server process.
cybersec-web-phase2  | Download https://deno.land/std@0.199.0/http/server.ts
cybersec-web-phase2  | Download https://deno.land/std@0.199.0/async/delay.ts
cybersec-db-phase2   |
cybersec-db-phase2   | The database cluster will be initialized with locale "en_US.utf8".
cybersec-db-phase2   | The default database encoding has accordingly been set to "UTF8".
cybersec-web-phase2  | Download https://deno.land/x/bcrypt@v0.4.1/mod.ts
cybersec-db-phase2   | The default text search configuration will be set to "english".
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/mod.ts
cybersec-db-phase2   |
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/mod.ts
cybersec-web-phase2  | Download https://deno.land/std@0.224.0/dotenv/load.ts
cybersec-web-phase2  | Download https://deno.land/x/bcrypt@v0.4.1/src/main.ts
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/index.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/client.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/client/error.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/pool.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/query/oid.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/query/transaction.ts
cybersec-web-phase2  | Download https://deno.land/std@0.224.0/dotenv/mod.ts
cybersec-web-phase2  | Download https://deno.land/x/bcrypt@v0.4.1/src/bcrypt/bcrypt.ts
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/external.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/connection/connection.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/connection/connection_params.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/query/query.ts
cybersec-db-phase2   | Data page checksums are enabled.
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/utils/utils.ts
cybersec-db-phase2   |
cybersec-db-phase2   | fixing permissions on existing directory /var/lib/postgresql/18/docker ... ok
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/utils/deferred.ts
cybersec-web-phase2  | Download https://deno.land/std@0.224.0/dotenv/parse.ts
cybersec-web-phase2  | Download https://deno.land/std@0.224.0/dotenv/stringify.ts
cybersec-web-phase2  | Download https://deno.land/x/bcrypt@v0.4.1/src/bcrypt/base64.ts
cybersec-db-phase2   | creating subdirectories ... ok
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/helpers/parseUtil.ts
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/helpers/typeAliases.ts
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/types.ts
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/ZodError.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/connection/packet.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/connection/message.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/connection/scram.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/connection/message_code.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/connection/auth.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/debug.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/query/encode.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/query/decode.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/fmt/meta.json
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/helpers/util.ts
cybersec-db-phase2   | selecting dynamic shared memory implementation ... posix
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/helpers/errorUtil.ts
cybersec-web-phase2  | Download https://deno.land/x/zod@v3.16.1/helpers/partialUtil.ts
cybersec-web-phase2  | Download https://jsr.io/@std/bytes/meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/encoding/meta.json
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/query/decoders.ts
cybersec-web-phase2  | Download https://deno.land/x/postgres@v0.19.5/query/array_parser.ts
cybersec-web-phase2  | Download https://jsr.io/@std/crypto/meta.json
cybersec-db-phase2   | selecting default "max_connections" ... 100
cybersec-db-phase2   | selecting default "shared_buffers" ... 128MB
cybersec-db-phase2   | selecting default time zone ... Etc/UTC
cybersec-db-phase2   | creating configuration files ... ok
cybersec-db-phase2   | running bootstrap script ... ok
cybersec-db-phase2   | performing post-bootstrap initialization ... ok
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3_meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/fmt/1.0.8_meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/bytes/1.0.6_meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/encoding/1.0.10_meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/crypto/1.0.5_meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/internal/meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/internal/1.0.12_meta.json
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/mod.ts
cybersec-web-phase2  | Download https://jsr.io/@std/fmt/1.0.8/colors.ts
cybersec-web-phase2  | Download https://jsr.io/@std/bytes/1.0.6/copy.ts
cybersec-web-phase2  | Download https://jsr.io/@std/encoding/1.0.10/base64.ts
cybersec-web-phase2  | Download https://jsr.io/@std/crypto/1.0.5/crypto.ts
cybersec-web-phase2  | Download https://jsr.io/@std/encoding/1.0.10/hex.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/basename.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/constants.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/dirname.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/extname.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/format.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/from_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/is_absolute.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/join.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/normalize.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/parse.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/relative.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/resolve.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/to_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/to_namespaced_path.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/common.ts
cybersec-db-phase2   | syncing data to disk ... ok
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/types.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/glob_to_regexp.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/is_glob.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/join_globs.ts
cybersec-db-phase2   |
cybersec-db-phase2   |
cybersec-db-phase2   | Success. You can now start the database server using:
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/normalize_glob.ts
cybersec-web-phase2  | Download https://jsr.io/@std/encoding/1.0.10/_common64.ts
cybersec-web-phase2  | Download https://jsr.io/@std/encoding/1.0.10/_common_detach.ts
cybersec-web-phase2  | Download https://jsr.io/@std/crypto/1.0.5/_wasm/mod.ts
cybersec-web-phase2  | Download https://jsr.io/@std/encoding/1.0.10/_common16.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/basename.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/basename.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/dirname.ts
cybersec-db-phase2   |
cybersec-db-phase2   |     pg_ctl -D /var/lib/postgresql/18/docker -l logfile start
cybersec-db-phase2   |
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/dirname.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/extname.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/extname.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/format.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/format.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/from_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/from_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/is_absolute.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/is_absolute.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/join.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/join.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/normalize.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/normalize.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/parse.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/parse.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/relative.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/relative.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/resolve.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/resolve.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/to_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/to_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/to_namespaced_path.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/to_namespaced_path.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/common.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/glob_to_regexp.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/glob_to_regexp.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/join_globs.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/join_globs.ts
cybersec-db-phase2   | initdb: warning: enabling "trust" authentication for local connections
cybersec-db-phase2   | initdb: hint: You can change this by editing pg_hba.conf or using the option -A, or --auth-local and --auth-host, the next time you run initdb.
cybersec-db-phase2   | waiting for server to start....2025-12-08 12:37:43.839 UTC [51] LOG:  starting PostgreSQL 18.1 (Debian 18.1-1.pgdg13+2) on x86_64-pc-linux-gnu, compiled by gcc (Debian 14.2.0-19) 14.2.0, 64-bit
cybersec-db-phase2   | 2025-12-08 12:37:43.843 UTC [51] LOG:  listening on Unix socket "/var/run/postgresql/.s.PGSQL.5432"
cybersec-db-phase2   | 2025-12-08 12:37:43.867 UTC [57] LOG:  database system was shut down at 2025-12-08 12:37:43 UTC
cybersec-db-phase2   | 2025-12-08 12:37:43.872 UTC [51] LOG:  database system is ready to accept connections
cybersec-db-phase2   |  done
cybersec-db-phase2   | server started
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/normalize_glob.ts
cybersec-db-phase2   |
cybersec-db-phase2   | /usr/local/bin/docker-entrypoint.sh: running /docker-entrypoint-initdb.d/init.sql
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/normalize_glob.ts
cybersec-db-phase2   | CREATE EXTENSION
cybersec-db-phase2   | CREATE EXTENSION
cybersec-db-phase2   | CREATE TABLE
cybersec-web-phase2  | Download https://jsr.io/@std/crypto/1.0.5/_wasm/lib/deno_std_wasm_crypto.mjs
cybersec-db-phase2   | CREATE TABLE
cybersec-db-phase2   | CREATE TABLE
cybersec-db-phase2   | CREATE TABLE
cybersec-db-phase2   | CREATE FUNCTION
cybersec-db-phase2   | CREATE TRIGGER
cybersec-db-phase2   | CREATE VIEW
cybersec-db-phase2   | CREATE FUNCTION
cybersec-db-phase2   | CREATE TABLE
cybersec-db-phase2   | INSERT 0 1
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/basename.ts
cybersec-db-phase2   | INSERT 0 1
cybersec-db-phase2   | INSERT 0 1
cybersec-db-phase2   | INSERT 0 1
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/strip_trailing_separators.ts
cybersec-db-phase2   | INSERT 0 1
cybersec-db-phase2   | INSERT 0 1
cybersec-db-phase2   | INSERT 0 1
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/_util.ts
cybersec-db-phase2   | INSERT 0 1
cybersec-db-phase2   | INSERT 0 1
cybersec-db-phase2   | INSERT 0 1
cybersec-db-phase2   |
cybersec-db-phase2   |
cybersec-db-phase2   | waiting for server to shut down....2025-12-08 12:37:44.322 UTC [51] LOG:  received fast shutdown request
cybersec-db-phase2   | 2025-12-08 12:37:44.327 UTC [51] LOG:  aborting any active transactions
cybersec-db-phase2   | 2025-12-08 12:37:44.333 UTC [51] LOG:  background worker "logical replication launcher" (PID 60) exited with exit code 1
cybersec-db-phase2   | 2025-12-08 12:37:44.334 UTC [55] LOG:  shutting down
cybersec-db-phase2   | 2025-12-08 12:37:44.340 UTC [55] LOG:  checkpoint starting: shutdown immediate
cybersec-db-phase2   | 2025-12-08 12:37:44.431 UTC [55] LOG:  checkpoint complete: wrote 135 buffers (0.8%), wrote 3 SLRU buffers; 0 WAL file(s) added, 0 removed, 0 recycled; write=0.023 s, sync=0.038 s, total=0.097 s; sync files=79, longest=0.004 s, average=0.001 s; distance=729 kB, estimate=729 kB; lsn=0/1815E18, redo lsn=0/1815E18
cybersec-db-phase2   | 2025-12-08 12:37:44.443 UTC [51] LOG:  database system is shut down
cybersec-db-phase2   |  done
cybersec-db-phase2   | server stopped
cybersec-db-phase2   |
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/from_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/normalize.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/normalize_string.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/relative.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/to_file_url.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/_common/glob_to_reg_exp.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/posix/constants.ts
cybersec-web-phase2  | Download https://jsr.io/@std/path/1.1.3/windows/constants.ts
cybersec-web-phase2  | Download https://jsr.io/@std/crypto/1.0.5/_wasm/lib/deno_std_wasm_crypto.internal.mjs
cybersec-web-phase2  | Download https://jsr.io/@std/internal/1.0.12/os.ts
cybersec-web-phase2  | Download https://jsr.io/@std/internal/1.0.12/_os.ts
cybersec-web-phase2  | 🔄 Attempting to connect to DB (try 1/10)...
cybersec-web-phase2  | ✅ Database connection successful!
cybersec-web-phase2  | Listening on http://localhost:8000/
---
**Single service:**
--
<img width="1960" height="833" alt="image" src="https://github.com/user-attachments/assets/ff8af014-7711-4f41-86c3-7f37d3a71880" />
---


**2.docker setup and run the compose yml file in browser**
---

<img width="1835" height="983" alt="image" src="https://github.com/user-attachments/assets/3d18b345-9e8c-4be6-881f-2bb214e8cbee" />



**3.Exploring the database schema and viewing user data**
---
<img width="1112" height="636" alt="image" src="https://github.com/user-attachments/assets/8eed1249-580b-4b93-b7f3-efd022acfaa6" />

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

# 5️⃣ OWASP ZAP Test Report ffor part1, part2 and phase2 (Attachment)
---
- [ZAP Report 1](zap-report1.md)
- [ZAP Report 2](zap-report2.md)
- [ZAP Report 3](zap-report3.md)
---


**Purpose:**  
- Attach or link your OWASP ZAP scan results.


  <img width="948" height="1349" alt="image" src="https://github.com/user-attachments/assets/414afd34-eca3-439f-857e-5bf66ffe91d1" />


---
**zap screen**
---

<img width="1431" height="1352" alt="image" src="https://github.com/user-attachments/assets/4fd66fb9-38ff-47ec-bca0-1a3a4fdc073d" />
---
<img width="1428" height="1068" alt="image" src="https://github.com/user-attachments/assets/83a6a10b-5511-4b26-9495-b695d31753d0" />

---

**ZAP testing**
---

**Step 3:Password Cracking**
---
<img width="1497" height="722" alt="image" src="https://github.com/user-attachments/assets/0be9e181-dc3d-49d3-8737-b74f1365ce2e" />
---
1 | whatsupdoc@looneytunes.tv |
Explanation:
This password follows a very common pattern: a simple English word + numbers. Such passwords exist in most public breach datasets, so CrackStation was able to find a match immediately.

<img width="1520" height="449" alt="image" src="https://github.com/user-attachments/assets/dfde1834-6d21-4e6f-bbea-de7eb532edc1" />

2 | doh@springfieldpower.net| 
Explanation:
This password follows a very common pattern: a simple English word + numbers. Such passwords exist in most public breach datasets, so CrackStation was able to find a match immediately.

<img width="1503" height="423" alt="image" src="https://github.com/user-attachments/assets/036c0721-b141-4241-84c1-7dfd062b5081" />

3 | darkknight@gothamwatch.org |
Explanation:
The password relates directly to the user’s fictional identity, making it predictable. Since many people use theme-based passwords, it already exists in CrackStation’s lookup tables.

<img width="1442" height="424" alt="image" src="https://github.com/user-attachments/assets/a6249bf6-7020-46b2-ae66-61ed76ca68ea" />

4 | iamyourfather@deathstar.gov  |
Explanation:
The password is a common phrase from popular culture and appears in leaked password lists. Since the hash was MD5 without salt, CrackStation could resolve it instantly.

<img width="1472" height="416" alt="image" src="https://github.com/user-attachments/assets/824986c8-ee6e-4ffa-863c-e09821017a92" />

5 | whysoserious@gothamchaos.net |

Explanation:
This password combines a simple word with a basic number pattern, making it extremely easy to crack. It was found immediately in CrackStation’s precomputed dictionary
<img width="1512" height="455" alt="image" src="https://github.com/user-attachments/assets/27dcf070-cf9c-40fb-b8c2-5da9bacbbad1" />

**[https://crackstation.net/ used for Password Cracking :](https://crackstation.net/)**

