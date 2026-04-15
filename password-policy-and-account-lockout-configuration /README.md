# Overview
As part of an ongoing effort to harden my IT Home Lab environment, I configured domain-wide password and account lockout policies on a Windows Server 2022 Domain Controller. This mirrors how security baselines are enforced in enterprise Active Directory environments, ensuring that all domain user accounts adhere to consistent, organisation-wide security standards.
# Environment
| Component| Details|
|----------|----------|
| Operating System   | Windows Server 2022  |
| Role | Active Directory Domain Controller   |
| Tool Used  |Group Policy Management Console (GPMC)   |
| Policy Scope | Default Domain Policy (domain-wide)   |

# Configuration Steps
# 1. Open Group Policy Management
I launched the Group Policy Management Console (GPMC) and located the Default Domain Policy, which is the designated Group Policy Object (GPO) for enforcing domain-wide security settings in Active Directory.
<img width="1032" height="603" alt="Screenshot from 2026-03-23 15-02-42" src="https://github.com/user-attachments/assets/61fd5bfd-be32-47e6-971b-69b2df2fc34d" />

# 2. Edit the Default Domain Policy
I right-clicked the Default Domain Policy and selected Edit to open it in the Group Policy Management Editor.
<img width="1032" height="603" alt="Screenshot from 2026-03-23 15-07-45" src="https://github.com/user-attachments/assets/442dbd5d-0cd7-4f68-94b0-fa7156a00bd7" />

# 3. Configure Password Policy
I navigated to the following path within the editor:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Password Policy
 I configured the following settings:

| Setting | Purpose |
|----------|----------|
|SettingPurposeMinimum Password Length  | LengthEnforces a minimum number of characters per password |
| Maximum Password Age  |  Requires users to change their password after a defined period  |
| Password Complexity Requirements  | Mandates a mix of character types (uppercase, lowercase, numbers, symbols)  |
|   Enforce Password History |  Prevents reuse of recent passwords   |

<img width="1032" height="603" alt="Screenshot from 2026-03-23 15-12-47" src="https://github.com/user-attachments/assets/907bba48-b79c-4614-82a6-cb3a524402ee" />

# 4. Configure Account Lockout Policy
I navigated to:
Computer Configuration > Policies > Windows Settings > Security Settings > Account Policies > Account Lockout Policy
I configured the following settings:

|Setting | Purpose|
|----------|----------|
|   Account Lockout Threshold  | Defines the number of failed login attempts before an account is locked   |
|   Account Lockout Duration |  Specifies how long an account remains locked before automatic unlock  |
|   Reset Account Lockout Counter |  Sets the time window after which failed attempt counters are reset   |

<img width="1032" height="603" alt="Screenshot from 2026-03-23 15-17-39" src="https://github.com/user-attachments/assets/55eb4a65-e0df-4e63-b1d8-d959d599948c" />

These controls provide defence against brute-force and password-guessing attacks by limiting repeated failed authentication attempts.

# 5. Apply the Policy
   
After saving the configuration, I forced an immediate policy refresh from an elevated Command Prompt:
gpupdate /force
<img width="1032" height="604" alt="Screenshot from 2026-03-23 15-20-11" src="https://github.com/user-attachments/assets/8f1dc0c1-6dab-4139-b70a-e5f797ff6319" />

# Validation
To confirm the policy was applied correctly and actively enforced across the domain, I used the Resultant Set of Policy tool:


This displayed the effective policies applied to the system, allowing me to verify that both the Password Policy and Account Lockout Policy settings were correctly active and reflected the intended configuration.

# Outcome

This configuration established a consistent, domain-wide security baseline for all user accounts, aligned with standard enterprise security practices. Key results include:

All domain users are subject to uniform password standards, reducing the risk of weak or reused credentials
Account lockout controls are in place to mitigate brute-force and password-spray attack vectors
Policy enforcement was verified using built-in Windows tools (gpupdate, rsop.msc)

This exercise provided practical, hands-on experience with Group Policy Management, Active Directory security configuration, and the enforcement of access control standards — skills directly applicable to roles in systems administration, IT security, and infrastructure support.
