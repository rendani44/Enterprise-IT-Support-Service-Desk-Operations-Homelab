

## Overview

This project documents the design, configuration, and validation of a secure departmental file share built on Windows Server File Services and Active Directory Domain Services (AD DS).

The objective was to provision a department-level share that enforces **least-privilege access**, **role-based permissions**, and **centralised access management** — principles consistent with enterprise IT security policy.

Permissions are applied in two deliberate layers:

- **Share-level permissions** act as a coarse network gateway, restricting who can reach the share at all.
- **NTFS permissions** on subfolders enforce granular, role-based access at the file system level.

This layered model prevents share-level permissions from becoming the effective access control mechanism — a common misconfiguration in environments where NTFS permissions are not consistently applied.

---

## Environment

| Component | Role |
|---|---|
| Windows Server | File Server (File and Storage Services role) |
| Server Manager | Share provisioning and management console |
| Active Directory Domain Services (AD DS) | Directory service for identity and group management |
| Active Directory Users and Computers (ADUC) | Security group creation and membership administration |
| Windows 10/11 Client Workstation (domain-joined) | End-user access validation |

---

## Implementation

### 1. Share Creation & Management

A single top-level share named **Finance Department** was provisioned via Server Manager using the New Share Wizard, hosted at the following local path on the file server:

```
C:\Share\Finance Department
```

A single top-level share was chosen deliberately. This design reduces administrative overhead, simplifies UNC path management for end users, and aligns with standard enterprise file server architecture — where departmental access is controlled beneath a single share entry point rather than through multiple individually permissioned shares.
<img width="1310" height="658" alt="Screenshot from 2026-04-17 22-11-18" src="https://github.com/user-attachments/assets/5a0d1a7a-bdd4-4a54-a9fe-8f5e14649b17" />

---

### 2. Share-Level Security (Least Privilege)

During share provisioning, the default **Everyone (Read)** permission assigned by Windows was explicitly removed. Permissions were restricted to:

- **Administrators** — Full Control
- **Designated Active Directory security group** — Read

Granting only Read at the share level is intentional. Share-level permissions serve as a coarse gateway only. Granular access distinctions — such as Modify vs. Read-only — are delegated entirely to NTFS permissions at the subfolder level, where access control is more precise and auditable.
<img width="1310" height="658" alt="Screenshot from 2026-04-17 23-38-51" src="https://github.com/user-attachments/assets/45ceb821-3946-468f-a66a-e65873884bf4" />

---

### 3. Folder Structure Design

A structured subfolder hierarchy was created within the Finance Department share to reflect operational business functions. Subfolders — including **Accounts Payable** — were organised to map directly to job roles, enabling role-based access control (RBAC) to be applied at the folder level rather than at the share root.

Structuring folders by business function rather than by user ensures that access boundaries remain stable as staff join, transfer, or leave the organisation. Access is managed by modifying security group membership — not by editing individual folder permissions — which reduces the risk of permission sprawl over time.
<img width="1310" height="658" alt="Screenshot from 2026-04-17 23-45-38" src="https://github.com/user-attachments/assets/7eac0382-8d03-44b9-b8d0-0a73de32299f" />

### 4. NTFS Permissions Using Security Groups

NTFS permissions on subfolders were applied exclusively through **Active Directory security groups**. No permissions were assigned directly to individual user accounts.

This enforces a clean separation between identity management (handled in ADUC) and resource access (enforced via NTFS ACLs), providing two key operational benefits:

1. **Access provisioning and revocation** requires only group membership changes — not folder permission edits.
2. **The ACL on each folder remains stable and auditable** regardless of staff turnover.

This approach is consistent with the principle that resource ACLs should not need to change when user assignments change.
<img width="1310" height="658" alt="Screenshot from 2026-04-17 23-55-20" src="https://github.com/user-attachments/assets/46e15aee-3469-489e-b6ba-d20e66b819d2" />

---

### 5. Access Verification from Client Workstation

End-to-end access was validated from a domain-joined Windows 10/11 client workstation using a **standard domain user account**. The user navigated to the share via UNC path and successfully accessed the Accounts Payable subfolder:

```
\\RENDANI-SA01\Finance Department
```

Successful access from the client workstation confirms that share-level permissions, NTFS permissions, and Active Directory group membership are all correctly aligned. This validation step is critical — it proves that the permission chain functions as intended from the perspective of an authenticated end user, not just from the server console.
<img width="1310" height="658" alt="Screenshot from 2026-04-18 02-27-38" src="https://github.com/user-attachments/assets/419a045c-f0ac-4671-aca7-582c088b4818" />

### 6. Client Access Optimisation

Following successful validation, the Finance Department share was **pinned to Quick Access** on the client workstation. This provides users with a consistent, persistent entry point to the share without requiring manual UNC navigation each session.

Quick Access pinning is a client-side convenience setting and does not affect share permissions, NTFS ACLs, or security group membership. It is applied post-validation to confirm the share is stable and ready for end-user consumption.
<img width="1310" height="658" alt="Screenshot from 2026-04-18 02-33-01" src="https://github.com/user-attachments/assets/9e2e236f-9795-4b8d-9363-8bac2db02c4b" />

## Skills Demonstrated

| Skill Area | Applied In This Project |
|---|---|
| Windows Server File Services | Provisioned and managed a departmental file share via Server Manager (File and Storage Services role) |
| Share-Level Permission Design | Removed default Everyone access; restricted share entry to Administrators and a designated AD security group |
| NTFS Permission Administration | Applied granular ACLs to subfolders using AD security groups, enforcing role-based access at the file system layer |
| Least-Privilege Enforcement | Implemented a two-layer permission model — permissive share boundary with restrictive NTFS controls — to minimise over-permissioning |
| Active Directory Administration | Created and managed security groups in ADUC; used group membership to control resource access rather than direct user assignment |
| Role-Based Access Control (RBAC) | Structured folder hierarchy and group assignments to reflect job function, enabling access to be governed by organisational role |
| End-to-End Access Validation | Confirmed correct permission enforcement from a domain-joined client workstation using a standard user account via UNC path |---

## Outcome

A secure and scalable file-sharing solution was successfully implemented using a single department-level share with layered access control. Share-level permissions were restricted, and NTFS permissions were enforced through Active Directory security groups to ensure least-privilege access to departmental data.

Through this implementation, hands-on experience was gained in configuring Windows Server file services, managing share and NTFS permissions, creating and administering Active Directory security groups, and applying role-based access control (RBAC). End-to-end validation from a domain-joined client workstation confirmed correct permission behavior and real-world usability.

Additional practical experience was gained by optimizing client access through pinning the verified network share to Quick Access, improving usability while maintaining all security controls. This project reflects real IT Support workflows used to securely manage shared resources in enterprise environments
