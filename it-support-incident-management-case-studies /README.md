# User Account Lockout — Incident Documentation
<img width="1360" height="620" alt="Screenshot from 2026-04-17 01-56-01" src="https://github.com/user-attachments/assets/a7fedeee-7ae4-4c27-8d83-a301f3445021" />

**Organisation:** Enterprise IT Support & Service Desk Operations
**Document Type:** Incident Record
**Prepared by:** IT Support Technician

---

## Incident Details

| Field | Value |
|---|---|
| **Incident Type** | User Account Lockout |
| **Category** | Access Management |
| **Sub-Category** | Authentication / Account Lockout |
| **Priority** | Medium (P3) |
| **Affected User** | Peter Khumalo |
| **Reported Via** | IT Service Management Platform (Spiceworks) |
## End-User Ticket Description

> Good morning,
>
> I am unable to log in to my workstation today. The system indicates that my account has been locked. Please advise on the next steps.
>
> Kind regards,
> Peter Khumalo
<img width="1360" height="604" alt="Screenshot from 2026-04-17 02-37-04" src="https://github.com/user-attachments/assets/0760c2dc-b5d5-43e7-b4fd-75b44489e34f" />
---

## Environment

- Windows Server 2022 (Domain Controller)
- Active Directory Domain Services (AD DS)
- Active Directory Users and Computers (ADUC)
- Domain-joined Windows 10/11 workstation
- IT Service Management Platform (Spiceworks)

---

## Incident Handling Procedure

### Step 1 — Classify the Incident as Security-Sensitive

User account lockouts can indicate repeated incorrect password attempts, a misconfigured device, or potential credential misuse. I treated this incident as security-sensitive from the outset and made no account changes prior to completing identity verification.

---

### Step 2 — Verify User Identity

Before taking any remediation action, I verified the user's identity by confirming that the request originated from the official ITSM platform and by cross-referencing the submitted name and username against Active Directory records.
<img width="1349" height="545" alt="Screenshot from 2026-04-17 04-10-44" src="https://github.com/user-attachments/assets/7769bbd2-a3b8-41f4-a59c-f5bb20324a68" />


---

### Step 3 — Confirm Account Lockout Status

I reviewed the user's account properties in Active Directory Users and Computers. The **Account is locked out** checkbox on the Account tab was selected, while the account showed no disabled or expired status. This confirmed the lockout was caused by failed authentication attempts rather than an administrative action.
<img width="1360" height="588" alt="Screenshot from 2026-04-17 02-47-01" src="https://github.com/user-attachments/assets/d671b1e0-3a3d-4ee6-bec2-8cb29f4f77bf" />

### Step 4 — Unlock the Account

After completing identity verification, I unlocked the account via the Account tab in the user's Active Directory properties. This restored the user's ability to authenticate while keeping all other account settings intact.
<img width="1360" height="588" alt="Screenshot from 2026-04-17 02-48-45" src="https://github.com/user-attachments/assets/8deafdbc-340d-47b9-9724-62655fd6b55f" />
---

### Step 5 — Reset the User Password

As a security best practice, I reset the user's password to invalidate any potentially compromised credentials. I enabled the **User must change password at next logon** option so that the user would establish a private, self-managed password on first login.
<img width="1360" height="588" alt="Screenshot from 2026-04-17 02-49-48" src="https://github.com/user-attachments/assets/f6f66ecc-45cb-4e7b-b06e-b8905dc220d2" />
---

### Step 6 — Controlled Verification of Access

To uphold least-privilege principles, I did not authenticate on behalf of the user. I provided the user with the temporary password and instructed them to log in independently. The user confirmed successful authentication via the ITSM ticket.

---
## Incident Resolution & Ticket Closure

The account lockout was resolved following identity verification and controlled account recovery. The user confirmed successful login and reported no further issues. The ticket was updated to **closed** in Spiceworks .
<img width="1360" height="566" alt="Screenshot from 2026-04-17 03-32-48" src="https://github.com/user-attachments/assets/1a658221-94cb-43e3-86e6-c9ee96f38ecd" />
 ---

## Documentation & Knowledge Recording

After resolving the incident and restoring user access, I documented the full incident lifecycle within the IT service management system. This included the verification steps, investigation findings, remediation actions, and confirmation of successful resolution.

Documenting the incident ensures consistency, accountability, and knowledge retention within the IT Support team. This record can be referenced for future account lockout incidents, audits, and onboarding of new support staff, reducing resolution time for similar issues.
<img width="1352" height="583" alt="Screenshot from 2026-04-17 04-24-07" src="https://github.com/user-attachments/assets/3212db7b-eee8-439b-ad83-62f7f0ee568a" />

## Skills Demonstrated

- Investigated and confirmed Active Directory user account lockout status using Active Directory Users and Computers (ADUC).
- Applied security‑first incident handling by verifying user identity before performing any account actions.
- Performed controlled account recovery by unlocking the user account and resetting credentials in accordance with security best practices.
- Enforced password hygiene by requiring the user to change their password at next logon.
- Followed proper Service Desk procedures, including incident validation, remediation, user confirmation, and ticket closure.



 
