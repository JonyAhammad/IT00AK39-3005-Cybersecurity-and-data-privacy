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

##  Guest (Not Logged In)

###  Can Do
- Can view landing page — `/`  
  - Observation: Page accessible  
  - Spec match: ✔ Yes

- Can view public resource list — `/resources`  
  - Observation: Resource list visible  
  - Spec match: ✔ Yes

- Can view booked resources without reserver identity — `/`  
  - Observation: No personal data shown  
  - Spec match: ✔ Yes (spec 8)

- Can access login page — `/login`  
  - Observation: Login form accessible  
  - Spec match: ✔ Yes

- Can access registration page — `/register`  
  - Observation: Registration available  
  - Spec match: ✔ Yes

---

###  Cannot Do
- Cannot access reservation page — `/reservation`  
  - Observation: Redirected to login  
  - Spec match: ✔ Yes

- Cannot access profile page — `/profile`  
  - Observation: Access denied  
  - Spec match: ✔ Yes

- Cannot access admin pages — `/admin/*`  
  - Observation: Blocked  
  - Spec match: ✔ Yes

- Cannot create reservations — `POST /api/reservations`  
  - Observation: Unauthorized  
  - Spec match: ✔ Yes

- Cannot access protected API endpoints — `/api/*`  
  - Observation: Access denied  
  - Spec match: ✔ Yes

---

## 🧑‍💼 Reserver (Authenticated User)

###  Can Do
- Can log in and log out — `/login`, `/logout`  
  - Observation: Works correctly  
  - Spec match: ✔ Yes

- Can book a resource — `/reservation`, `POST /api/reservations`  
  - Observation: Booking successful  
  - Spec match: ✔ Yes

- Can view own profile and reservations — `/profile`  
  - Observation: Only own data visible  
  - Spec match: ✔ Yes

- Can list resources — `/resources`  
  - Observation: Accessible  
  - Spec match: ✔ Yes

- Can access reserver APIs — `/api/reservations`  
  - Observation: Limited to own data  
  - Spec match: ✔ Yes

---

###  Cannot Do
- Cannot access admin dashboard — `/admin`  
  - Observation: Access denied  
  - Spec match: ✔ Yes

- Cannot manage users — `/api/admin/users`  
  - Observation: Unauthorized  
  - Spec match: ✔ Yes

- Cannot delete other users — `/api/admin/users/:id`  
  - Observation: Blocked  
  - Spec match: ✔ Yes

- Cannot modify resources — `/api/admin/resources`  
  - Observation: Blocked  
  - Spec match: ✔ Yes

- Cannot escalate privileges via form or API tampering  
  - Observation: Role unchanged  
  - Spec match: ✔ Yes

---

##  Administrator

###  Can Do
- Can access admin dashboard — `/admin`  
  - Observation: Accessible  
  - Spec match: ✔ Yes

- Can add, modify, and delete resources — `/admin/resources/*`  
  - Observation: Actions successful  
  - Spec match: ✔ Yes

- Can manage all reservations — `/admin/reservations`  
  - Observation: Full access  
  - Spec match: ✔ Yes

- Can delete reservers — `/admin/users/delete/:id`  
  - Observation: Deletion successful  
  - Spec match: ✔ Yes

- Can view all users — `/admin/users`  
  - Observation: User list visible  
  - Spec match: ✔ Yes (spec 4)

---

### ❌ Cannot Do / Observations
- No unnecessary permissions detected  
- No excessive data exposure found  
- No admin-only endpoints accessible by other roles  

---

##  Hidden Endpoint Discovery

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




