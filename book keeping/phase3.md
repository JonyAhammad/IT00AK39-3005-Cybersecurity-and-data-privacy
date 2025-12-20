#  Authorization Testing Report – Phase 3

## Tester(s)
- **Jony Ahammad**
- **Rex**

---

##  Purpose of the Test

The purpose of this authorization testing is to verify that **role-based access control (RBAC)** is correctly implemented in the **Phase 3 Booking System**.

The test confirms that:
- Guests cannot access protected content
- Reservers cannot perform administrator actions
- Administrators have full control without unnecessary exposure
- Authorization is enforced at the backend level
- No hidden endpoints or authorization bypasses exist

System behavior is evaluated against the official project specifications (points 1–8).

---

##  Test Methodology

- **Approach:** Gray-box testing  
- **Techniques:**
  - Browser-based manual testing
  - URL manipulation
  - OWASP ZAP authenticated scans
  - Gobuster and wfuzz endpoint discovery
- **Roles Tested:**
  - Guest
  - Reserver
  - Administrator

---

### ✅ Guest — Allowed Actions

| Action | Endpoint | Behavior | Spec OK? | Notes |
|--------|---------|----------|----------|-------|
| View public resource list | `/` | Works, shows resources without names | ✔️ Yes | Matches GDPR requirement (spec #8) |
| Access login page | `/login` | Works | ✔️ Yes | - |
| Access registration page | `/register` | Works | ✔️ Yes | - |
| Access public API resources | `/api/resources` | Returns data | ❌ No | Data exposure vulnerability |

### ❌ Guest — Blocked Actions

| Action | Endpoint | Behavior | Spec OK? |
|--------|---------|----------|----------|
| Access profile | `/profile` | Not Found | ✔️ Yes |
| Access reservation page | `/reservation` | Unauthorized | ✔️ Yes |
| Access admin dashboard | `/admin` | Not Found | ✔️ Yes |
| Access admin user list | `/admin/users` | Not Found | ✔️ Yes |
| Access admin resources | `/admin/resources` | Not Found | ✔️ Yes |
| Access reservations API | `/api/reservations` | Protected (returns nothing) | ✔️ Yes |
| Access admin user API | `/api/admin/users` | Not Found | ✔️ Yes |

---

## 2. Reserver (Logged-In Normal User)

### ✅ Reserver — Allowed Actions

| Action | Endpoint | Behavior | Spec OK? | Notes |
|--------|---------|----------|----------|-------|
| Login | `/login` | Works | ✔️ Yes | - |
| Register | `/register` | Works | ✔️ Yes | - |
| Access reservation page | `/reservation` | Works | ✔️ Yes | Can book resources |
| View resources (API) | `/api/resources` | Returns data | ✔️ Yes | Reserver can see available resources |
| View reservations (API) | `/api/reservations` | Returns data | ✔️ Yes | Can view own or all reservations |

### ❌ Reserver — Blocked / Incorrect Actions

| Action | Endpoint | Behavior | Spec OK? | Notes |
|--------|---------|----------|----------|-------|
| Access profile | `/profile` | Not Found (404) | ❌ No | BUG: Reserver should have a profile page |
| Access admin pages | `/admin/*` | 404 – “The process failed” | ✔️ Yes | Correctly blocked, though 403 preferred |
| Access admin API | `/api/admin/users` | 404 – “The process failed” | ✔️ Yes | Correctly protected |

---

## 3. Administrator (Logged-In Admin User)

### ✅ Admin — Allowed Actions

| Action | Endpoint | Behavior | Spec OK? | Notes |
|--------|---------|----------|----------|-------|
| View homepage | `/` | Works, names hidden | ✔️ Yes | Good privacy |
| Login | `/login` | Works | ✔️ Yes | - |
| Register | `/register` | Works | ✔️ Yes | - |
| Access reservation UI | `/reservation` | Works | ✔️ Yes | - |
| List resources (API) | `/api/resources` | Returns data | ✔️ Yes | - |
| Create resource | `POST /api/resources` | Works | ✔️ Yes | Admin can add resources |
| Modify resource | `PUT /api/resources/1` | Works | ✔️ Yes | Admin can edit resources |
| View all reservations | `/api/reservations` | Works | ✔️ Yes | Admin access allowed |

### ❌ Admin — Unexpected Limitations / Bugs

| Action | Endpoint | Behavior | Spec OK? | Notes |
|--------|---------|----------|----------|-------|
| Access admin dashboard | `/admin` | Not Found | ❌ No | Admin UI missing |
| View users (UI) | `/admin/users` | Not Found | ❌ No | Required by spec |
| Manage resources (UI) | `/admin/resources` | Not Found | ❌ No | UI does not exist |
| Delete resource | `DELETE /api/resources/1` | ❌ Error | ❌ No | Admin must delete resources |
| View users (API) | `GET /api/admin/users` | Not Found | ❌ No | Must exist per spec |
| Delete user | `DELETE /api/admin/users/1` | Not Found | ❌ No | Admin cannot remove reservers |


---

# Phase 3 — Hidden Directory & Endpoint Discovery (Gobuster + wfuzz)

### Tools Used
- OWASP ZAP
- Gobuster
- wfuzz

### Findings
- All discovered endpoints were protected
- No IDOR vulnerabilities detected
- No authorization bypasses found

  
**connecting to debien and running into powersheel**
--

<img width="1635" height="1359" alt="image" src="https://github.com/user-attachments/assets/596d8853-4592-4f93-9770-e357a06bf6a0" />

**Run the booking website and reserve and test**
--
<img width="1458" height="1185" alt="image" src="https://github.com/user-attachments/assets/e8d03fac-6716-464c-8c8f-b772a5db36d8" />


**zap test**
--
<img width="1421" height="1341" alt="image" src="https://github.com/user-attachments/assets/48269cca-e877-4f46-bb30-4c98c011e365" />

[ZAP Report 4:](zap-report4.md)
--
**database**
--
<img width="1374" height="347" alt="image" src="https://github.com/user-attachments/assets/a900addf-c351-4919-ace3-47c6402f1cd7" />




<img width="2462" height="1003" alt="image" src="https://github.com/user-attachments/assets/c8223d38-72f9-4d4f-905e-d68e5d09a64b" />

**manage reservation update, delete, cancel**
--
<img width="2158" height="985" alt="image" src="https://github.com/user-attachments/assets/fade64df-0c2d-40e6-b8ca-549160a0f0b6" />

**manage reservation as adminstratorl**
---
<img width="1367" height="819" alt="image" src="https://github.com/user-attachments/assets/4d06f650-ceb6-43d9-a247-6ec0c6a56d3c" />

**Gobuster / wfuzz / ffuf install**
--

<img width="1894" height="877" alt="image" src="https://github.com/user-attachments/assets/90de23c8-3fdc-4fe6-9ddc-e65561f637c7" />

**dictionary attack**
--

<img width="1838" height="604" alt="image" src="https://github.com/user-attachments/assets/3e616a91-8b90-4837-a6ff-c61d4ca159b3" />

**api test** 
--
<img width="1721" height="612" alt="image" src="https://github.com/user-attachments/assets/3faba64b-7743-4deb-a4e4-cf8d0d77cf66" />
<img width="1622" height="538" alt="image" src="https://github.com/user-attachments/assets/57f3fea6-7cd1-4456-abf4-1dfcc88bea30" />

**user api test**
--
<img width="870" height="702" alt="image" src="https://github.com/user-attachments/assets/161a63a7-09ff-40ea-a953-3ef412bf08b6" />

**reservetion api test**
--
<img width="922" height="785" alt="image" src="https://github.com/user-attachments/assets/1e2b412d-7337-4d16-8453-334e0230a069" />

**resources api test**
--
<img width="960" height="969" alt="image" src="https://github.com/user-attachments/assets/be78b295-e093-4e91-8b4e-0fcf19318883" />




