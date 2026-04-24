# Backup & Disaster Recovery — Windows Server Backup (WSB)

> **Environment:** Windows Server 2022 | Oracle VirtualBox |

---

## Table of Contents

1. [Project Overview](#1-project-overview)
2. [Lab Environment](#2-lab-environment)
3. [Installing Windows Server Backup](#3-installing-windows-server-backup)
4. [Configuring Full Server Backup](#4-configuring-full-server-backup)
5. [System State Backup - Active Directory Protection](#5-system-state-backup--active-directory-protection)
6. [Restore Test -Simulated Data Loss and Recovery](#6-restore-test--simulated-data-loss-and-recovery)
7. [Backup Architecture - 3-2-1 Rule](#7-backup-architecture--3-2-1-rule)
8. [Task Completion Summary](#8-task-completion-summary)
9. [Skills Demonstrated](#9-skills-demonstrated)
10. [Next Steps](#10-next-steps)

---

## 1. Project Overview

In this lab I implemented a structured backup and disaster recovery solution on a Windows Server 2022 domain controller. The objective was to go beyond simply installing a backup tool - I designed a solution that mirrors how IT support teams protect Active Directory environments in small to medium business environments, following the industry-standard 3-2-1 backup rule.

The three real-world scenarios I built this lab around are:

- **Accidental file or folder deletion** - a user permanently deletes an important shared folder and its contents
- **Active Directory data loss** - Organisational Units, user accounts, or Group Policy Objects are accidentally removed
- **Catastrophic server failure or ransomware** - the entire server needs to be recovered from a clean backup

Understanding how to configure, schedule, and - most critically - successfully restore from a backup is one of the most valued practical skills in IT Support and Help Desk roles. This lab demonstrates that skill end to end with documented, verified results.

---

## 2. Lab Environment

| Component | Details |
|---|---|
| Server OS | Windows Server 2022 - Domain Controller (RENDANI-SA01) |
| Client VMs | Windows 10 / Windows 11 - domain-joined workstations |
| AD Domain | Enterprise-simulated multi-machine environment |
| Backup Tool | Windows Server Backup (WSB) - built-in Windows Server feature |
| CLI Tool | wbadmin.exe - used for System State backups via PowerShell |
| Backup Destination | 50 GB dedicated virtual disk -E: BackupDrive |

> **Why a separate disk?** I intentionally isolated the backup destination onto a dedicated virtual disk separate from the OS drive. If the OS drive fails or ransomware encrypts C:, the backup on E: remains untouched. This mirrors enterprise backup storage design.
<img width="1311" height="653" alt="Screenshot from 2026-04-22 15-41-15" src="https://github.com/user-attachments/assets/e6287ed3-2b37-4da7-9793-2571958f09d5" />

## 3. Installing Windows Server Backup

Windows Server Backup (WSB) is a built-in feature of Windows Server 2022 - no download or third-party software is required. I installed it using PowerShell running as Administrator on the domain controller the installation command i used was # Install Windows Server Backup with management tools
Install-WindowsFeature Windows-Server-Backup -IncludeManagementTools .
### 3.2 - Verification

After installation I verified WSB was available :
 Opened **Server Manager** → **Tools** → confirmed **Windows Server Backup** appeared in the tools list
<img width="1308" height="653" alt="Screenshot from 2026-04-24 22-32-46" src="https://github.com/user-attachments/assets/ea0c01ac-7cb6-4d05-9a9c-3082f6e77f22" />

## 4. Configuring Full Server Backup

I configured a Full Server backup to run automatically every night at 11:00 PM. A Full Server backup captures everything on the domain controller - the operating system, Active Directory Domain Services, Group Policy Objects, DNS configuration, shared folders, NTFS permissions, and all system settings. This is the primary recovery option for catastrophic server failure or ransomware.
### 4.1 - What a Full Server Backup Protects

| Protected Component | Why It Matters |
|---|---|
| Windows Server 2022 OS files | Required to boot and operate the server |
| Active Directory (AD DS) | All user accounts, groups, and Organisational Units |
| Group Policy Objects (GPOs) | Password policies, security baselines, user environment settings |
| DNS zones and records | Domain name resolution for all clients |
| Shared folders and NTFS permissions | Departmental file access structures |
| Print Server configuration | Deployed printers and sharing settings |
| Windows Registry | All system and application configuration |

### 4.2 - Configuring the Backup Schedule

I configured the schedule through the Windows Server Backup console:

1. Opened **Server Manager** → **Tools** → **Windows Server Backup**
2. In the right-hand **Actions** panel, clicked **Backup Schedule...**
3. Selected **Full server (recommended)** as the backup configuration
4. Set the schedule to **Once a day at 11:00 PM** - running after hours to avoid any performance impact during business hours
5. Selected **E: BackupDrive** as the dedicated backup destination
6. Confirmed the configuration - WSB formatted E: BackupDrive as a managed backup volume and confirmed the schedule was active

> **Note:** When WSB takes ownership of the backup disk, it disappears from normal File Explorer access. This is intentional - WSB manages the disk entirely to prevent accidental modification or deletion of backup data.
<img width="1311" height="653" alt="Screenshot from 2026-04-22 15-47-48" src="https://github.com/user-attachments/assets/6f11dae0-5ace-4eab-84e5-74f45adb6ec0" />


### 4.3 - Manual Backup Run (Verification)

Before relying on the schedule, I ran a manual backup immediately to verify the configuration was working and to establish the first restore point.

1. In WSB, clicked **Backup Once...** → **Different options** → **Next**
2. Selected **Full server** → **Local drives** → selected **E: BackupDrive** → clicked **Backup**
<img width="1311" height="653" alt="Screenshot from 2026-04-22 23-05-47" src="https://github.com/user-attachments/assets/ec0b9fce-49e8-418c-8235-0e41d6fa2f7c" />

  ### 5.3 - Running the System State Backup

I ran the System State backup from an elevated PowerShell session using the `wbadmin` command-line tool:

```powershell
# Run System State backup targeting the dedicated backup drive
wbadmin start systemstatebackup -backupTarget:E: -quiet
```

**Command breakdown:**

| Parameter | Purpose |
|---|---|
| `wbadmin` | Windows Server Backup command-line tool |
| `start systemstatebackup` | Initiates a System State backup job |
| `-backupTarget:E:` | Directs the backup output to E: BackupDrive |
| `-quiet` | Runs without confirmation prompts - suitable for scripting and automation |

The output confirmed the backup completed with the message:
`Backup of System State, was successful.` 
<img width="1311" height="653" alt="Screenshot from 2026-04-22 16-21-37" src="https://github.com/user-attachments/assets/942b5b05-99ba-43aa-8596-d9fb0f436b43" />

<img width="1311" height="653" alt="Screenshot from 2026-04-22 18-38-10" src="https://github.com/user-attachments/assets/6f00f6b3-0b51-4c13-852b-c46e67cd3057" />

