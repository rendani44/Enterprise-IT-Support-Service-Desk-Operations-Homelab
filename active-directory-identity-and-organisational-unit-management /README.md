

# Creating Users, Security Groups, and Organizational Units 

## Overview

This project documents the process of creating and managing **Organizational Units (OUs), security groups, and user accounts** within a Windows Server 2022 Active Directory environment. The goal of this lab was to simulate real-world identity and access management tasks commonly performed by IT Support and Help Desk professionals in enterprise environments.

By completing this project, I practiced structuring Active Directory correctly, implementing role-based access control, and managing the user lifecycle in a secure and organized manner.

---

## Environment Used

- **Windows Server 2022** (Domain Controller)
- **Active Directory Domain Services (AD DS)**
- **Active Directory Users and Computers (ADUC)**
- Domain-joined Windows 10/11 client machines
- Virtualized lab environment (home lab)

## Step 1: Creating Organizational Units (OUs)
<img width="1353" height="685" alt="Screenshot from 2026-03-23 02-10-06" src="https://github.com/user-attachments/assets/272edcff-39e9-4cf0-a2ef-972f8aa3b99d" />
I began by opening **Active Directory Users and Computers (ADUC)** from the Windows Administrative Tools menu.
Before creating any users or groups, I designed and implemented a clean and organized **Organizational Unit (OU) structure**. This included dedicated OUs such as **Users**, **Groups**, and department-specific containers.
<img width="1025" height="601" alt="Screenshot from 2026-03-23 04-41-15" src="https://github.com/user-attachments/assets/72eef62a-c6f0-46e1-91b1-5bf519e489c6" />

Creating OUs first is a best practice because it helps maintain order within the domain and allows Group Policies to be applied in a controlled and structured manner. To create each OU, I right-clicked the domain name, selected **New**, then **Organizational Unit**, and completed the naming and configuration process.

## Step 2: Creating Security Groups

After the OU structure was in place, I proceeded to create **security groups**, which are essential for managing access and permissions across the network. Within the designated **Groups OU**, I created multiple security groups using clear and meaningful names such as **IT Support** and **HR Staff**.

All groups were created as **Global Security Groups**, which are recommended for managing access within a single-domain environment. These groups were later used to assign permissions to resources and control user access based on job roles.

<img width="1025" height="601" alt="Screenshot from 2026-03-23 04-41-35" src="https://github.com/user-attachments/assets/4f0610cb-c130-4a87-878a-6e35fd88333e" />

## Step 3: Creating User Accounts

With the security groups created, I then created user accounts for individuals who would be part of the domain. Inside the **Users OU**, I added new users by selecting **New → User** and entering the required information, including first name, last name, and user logon name.

Each account was configured with a secure password, and I enabled the option **“User must change password at next logon”** to follow best security practices. This mirrors real-world onboarding procedures used in professional IT environments.

<img width="1025" height="601" alt="Screenshot from 2026-03-23 04-44-54" src="https://github.com/user-attachments/assets/267b1d4d-fff3-4ed4-b991-c85d559a4eb2" />

once the user accounts were created, I assigned users to their appropriate security groups based on their roles. This was done by opening the group’s properties and adding users through the **Members** tab.

Assigning users to groups instead of granting permissions directly to individual accounts ensures scalability, easier management, and consistent access control. This approach reflects standard role-based access control (RBAC) practices used in enterprise environments.

## Step 5: Verification and Validation

To finalize the configuration, I performed several verification checks to ensure everything was set up correctly. I reviewed each user’s **Member Of** tab to confirm proper group membership and inspected each OU to verify that objects were placed in the correct containers.
<img width="1360" height="564" alt="Screenshot from 2026-04-13 00-22-06" src="https://github.com/user-attachments/assets/c18bb106-cf2f-4416-bc47-26454242aa4c" />

These validation steps ensured that users received the appropriate permissions and that the Active Directory structure followed best practices. Authentication and access behavior were also tested from domain-joined client machines.

## Skills Practiced

Through this lab, I gained hands-on experience in:

- Active Directory user and group management  
- Organizational Unit (OU) design and best practices  
- Role-based access control (RBAC)  
- User onboarding and account configuration  
- Security group creation and management  
- Identity and access management fundamentals  
- Verification and troubleshooting of group memberships  

---

## Outcome and Learning Reflection

This project strengthened my understanding of how real IT environments manage user identities and access permissions using Active Directory. I learned how to properly organize directory objects, implement security groups for access control, and follow best practices for user onboarding and verification.

Overall, this lab closely reflects real-world IT Support and Help Desk responsibilities and helped me build confidence in managing Active Directory environments commonly found in enterprise organizations.

