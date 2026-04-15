# Overview
As part of managing the user lifecycle in my IT Home Lab, I implemented a structured offboarding process for departing employees using Active Directory Users and Computers (ADUC). This process ensures that all domain access is revoked promptly and systematically when a user leaves the organisation, following the same steps used in professional enterprise IT environments.
# Environment

|Component| Details|
|----------|----------|
|Operating System  | Windows Server 2022   |
| Role   | Active Directory Domain Controller |
| Tool Used |   Active Directory Users and Computers (ADUC) |
|Policy Scope|    Domain user accounts|

# Offboarding Steps
# 1. Locate the User Account
I opened Active Directory Users and Computers (ADUC) and navigated to the appropriate Organisational Unit (OU) to locate the departing user's account.

# 2. Disable the Account
I right-clicked the user account and selected Disable Account.
Disabling the account immediately prevents the user from authenticating against the domain — blocking access to all domain-joined computers and network resources.
<img width="1022" height="606" alt="Screenshot from 2026-03-23 05-32-26" src="https://github.com/user-attachments/assets/936165d7-ad07-41d6-9076-410e0aac15f5" />

Verification: A downward-pointing arrow icon appears on the account object in ADUC, confirming the account has been successfully disabled.
<img width="1022" height="606" alt="Screenshot from 2026-03-23 05-32-58" src="https://github.com/user-attachments/assets/73a299c2-b183-4049-a497-2d7d7c4cd33b" />

# 3. Reset the Account Password
I right-clicked the user account and selected Reset Password, then set a randomised, secure password.
This step ensures the account cannot be accessed — even if it were temporarily re-enabled — providing an additional layer of security throughout the offboarding window.
<img width="1022" height="606" alt="Screenshot from 2026-03-23 05-42-32" src="https://github.com/user-attachments/assets/2ad1fcff-27cc-47e7-8ea0-57bb448fc6ff" />

# 4. Remove Group Memberships
I opened the user's Properties, navigated to the Member Of tab, and removed the account from all assigned security groups, including:

Departmental groups
<img width="1022" height="606" alt="Screenshot from 2026-03-23 05-45-04" src="https://github.com/user-attachments/assets/4d2679f5-8b38-492c-9182-930f46fc8b8e" />
Removing all group memberships ensures the user retains no residual permissions or access rights within the domain.

# 5. Move the Account to the Disabled Users OU
After completing the above steps, I moved the account from its current OU into a dedicated Disabled Users OU by dragging and dropping it within ADUC.
This OU serves as a holding area for inactive accounts, keeping the directory organised and clearly separated from active employee accounts — a standard practice in enterprise Active Directory environments.
<img width="1022" height="606" alt="Screenshot from 2026-03-23 05-47-18" src="https://github.com/user-attachments/assets/6abb6fd4-5de9-4c5a-9270-13ae98c13a6e" />

# 6. Delete the Account After the Retention Period
The account remains in the Disabled Users OU for the duration of the retention period — typically 30 to 90 days in real-world environments — to allow for any access recovery or audit requirements.
Once the retention period has elapsed, I navigated to the Disabled Users OU, right-clicked the account, and selected Delete to permanently remove it from Active Directory.
<img width="1022" height="606" alt="Screenshot from 2026-03-23 05-48-50" src="https://github.com/user-attachments/assets/18807a57-b447-4176-be1c-051680b2583d" />

# Outcome
This process established a consistent, security-focused offboarding procedure aligned with enterprise IT and access control standards. Key results include:

Domain access is revoked immediately upon account disablement
Password reset prevents any residual authentication risk during the retention window
Group membership removal eliminates all permission assignments within the domain
Organised archival in a dedicated OU maintains directory hygiene and supports audit readiness
Permanent deletion is performed only after an appropriate retention period, consistent with real-world IT policy

This exercise provided hands-on experience with user lifecycle management, access control, and Active Directory administration — skills directly applicable to roles in IT support, systems administration, and identity and access management (IAM).

