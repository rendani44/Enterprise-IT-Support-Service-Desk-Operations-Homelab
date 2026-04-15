# PROJECT OVERVIEW


In this home lab project, I planned, deployed, and validated a fully functional centralised Print Server on a Windows Server 2022 domain controller — replicating the kind of enterprise print infrastructure found in mid-to-large organisations. The goal was not just to follow steps, but to make deliberate technical decisions at each stage and understand why each one matters in a production environment. This project covers role installation, driver architecture management, TCP/IP network printer configuration, Active Directory integration, and rigorous end-to-end testing from a client machine — the complete lifecycle of an enterprise printer deployment.
Every configuration decision documented here has a real-world justification. This is the approach I bring to every lab project and, ultimately, to every professional role.

# Step 1  —  Installing the Print Server Role

I began by opening Server Manager and launching the Add Roles and Features wizard. Under Server Roles, I selected Print and Document Services and then chose the Print Server sub-role. This installs the core print management engine on the server — giving it the ability to host print queues, manage drivers centrally, and share printers across the entire domain network. Once the installation completed, the server was transformed from a standard domain controller into a fully capable enterprise print management server, ready to support every printer in the environment from a single console.

<img width="1366" height="585" alt="Screenshot from 2026-04-14 00-02-29" src="https://github.com/user-attachments/assets/e5da34f5-cf71-4f19-bcc8-8cd2f8f5989e" />


# Step 2  —  Opening the Print Management Console
With the role installed, I navigated to Server Manager → Tools → Print Management to open the centralised management console. This single-pane interface is where all print infrastructure is controlled — printers, drivers, queues, ports, and deployment policies are all managed from here. In a real enterprise environment, a sysadmin would use this console to oversee dozens or hundreds of printers across multiple sites without ever leaving their desk. Understanding this console is a core competency for any IT Support or Help Desk professional working in a Windows Server environment.

<img width="1366" height="582" alt="Screenshot from 2026-04-13 21-16-17" src="https://github.com/user-attachments/assets/2aa802de-c892-4426-a7d6-25852dd448df" />


# Step 3  —  Adding Printer Drivers — 64-bit and 32-bit
I right-clicked the Drivers node under my server in the Print Management Console and selected Add Driver. When prompted to select processor architectures, I chose both x64 (64-bit) and x86 (32-bit). This is a deliberate enterprise decision, not a default. In real organisations, client machines are not uniform — there are always legacy 32-bit systems running alongside modern 64-bit workstations. By pre-loading both driver versions on the print server, Windows automatically pushes the correct driver to any connecting client without the user or helpdesk needing to install anything manually. This single step eliminates an entire category of printer compatibility tickets.

# Step 4  —  Installing the Driver Package
I navigated to the folder containing the prepared vendor driver files and completed the installation through the wizard. Sourcing and staging the correct driver package before beginning configuration is a discipline that mirrors real IT operations. Incorrect, outdated, or mismatched drivers are among the most common root causes of print queue failures in enterprise environments. Having the right driver ready — verified against the printer model and operating system — before touching the server saves significant troubleshooting time and reflects the kind of preparation that separates junior engineers from strong candidates. The installation completed successfully and the driver appeared in the Drivers list ready for assignment.

<img width="1366" height="585" alt="Screenshot from 2026-04-13 22-09-43" src="https://github.com/user-attachments/assets/f51ca8b9-a155-4fa1-8dcb-c15f07427d93" />

<img width="1366" height="585" alt="Screenshot from 2026-04-13 22-18-26" src="https://github.com/user-attachments/assets/05fcc6bd-22eb-4bff-8d21-9847757afdb5" />


# Step 5  —  Adding the Printer via TCP/IP Network Wizard
I right-clicked the Printers node in Print Management and selected Add Printer, which launched the Network Printer Installation Wizard. I entered the static IP address assigned to the printer and selected TCP/IP Device as the connection type. Using a static IP address here is a non-negotiable requirement, not a preference. If the printer were on a dynamic DHCP lease, its IP address could change after any network restart or DHCP renewal — silently breaking the connection between the print server and the device and generating a wave of helpdesk calls. Configuring network printers with static IPs is standard practice in every enterprise environment, and this project reflects that discipline.

<img width="1366" height="585" alt="Screenshot from 2026-04-13 22-20-56" src="https://github.com/user-attachments/assets/eedf7beb-fd5a-487e-b3b3-ada785df1ced" />


# Step 6  —  Configuring the Share Name and Location Tag
Inside the printer's properties, I navigated to the Sharing tab, enabled printer sharing, and assigned a clear and descriptive share name. I then set the Location field to Floor 1. These details may appear minor in a single-printer lab setup, but in a real organisation with printers spread across multiple floors, buildings, or sites, they are operationally critical. A well-named share and an accurate location tag allow users to find the right printer without contacting the helpdesk, and allow technicians to identify the exact physical device during troubleshooting without walking the building. Good naming conventions at deployment time directly reduce support ticket volume over the life of the deployment.

<img width="1366" height="585" alt="Screenshot from 2026-04-13 22-22-48" src="https://github.com/user-attachments/assets/5ed4238d-6c8a-479a-aaed-ef7f3589d319" />


# Step 7  —  Publishing the Printer to Active Directory
With sharing configured, I right-clicked the printer in the Print Management Console and selected List in Directory. This action publishes the printer as a searchable object within Active Directory, making it discoverable by all domain-joined users and computers across the network. In a large organisation, this is the mechanism that enables self-service printer connection — users can search for printers by name or location through the network without any admin involvement. It also enables Group Policy-based automated deployment, where printers are pushed to specific computers or organisational units silently in the background. Understanding the relationship between print management and Active Directory is a differentiating skill for anyone moving beyond basic Help Desk work.

<img width="1366" height="585" alt="Screenshot from 2026-04-13 22-31-46" src="https://github.com/user-attachments/assets/2f77161a-75b3-4a9f-82b5-0111b4662e50" />


# Step 8  —  End-to-End Validation from a Client Machine
To confirm the full deployment was working correctly, I logged into a domain-joined Windows 10/11 machine using a standard test user account — not an admin account. I verified that the printer appeared correctly under Devices and Printers and then sent a test page. The test page printed successfully, confirming that the entire print path was functional end-to-end: from the print server hosting the queue, across the network to the physical device, and accessible from the perspective of an ordinary domain user. Validating from a non-admin user account is an important habit. Many deployments appear to work when tested by an administrator but fail for standard users due to permission gaps — catching that distinction in testing prevents it from becoming a production incident.

<img width="1366" height="585" alt="Screenshot from 2026-04-13 23-04-42" src="https://github.com/user-attachments/assets/16dd4676-1ad8-42f3-bb9f-381e3ff998fb" />



# Key Takeaways & Lessons Learned
    • Dual-architecture drivers:  Selecting both 64-bit and 32-bit drivers from the start prevents compatibility failures across mixed client environments — a common oversight that generates unnecessary helpdesk tickets.
    • Static IP is non-negotiable:  Dynamic IPs would silently break print server connectivity after any network change. Every network printer in a production environment must have a reserved or static IP address.
    • Active Directory publishing:  Listing the printer in AD transforms a manually managed resource into a self-service, policy-deployable asset — a key operational improvement in organisations at scale.
    • Test as a standard user:  Validating from a non-admin account catches permission gaps before they reach production. Many deployments work for admins but fail for regular users — this step closes that gap.
    • Location tags are operational infrastructure:  In any environment with more than a handful of printers, accurate location metadata directly reduces helpdesk call volume and physical troubleshooting time.

# What This Project Demonstrates About How I Work
This project reflects the structured, decision-driven approach I bring to IT work. I did not simply click through a wizard and call it done. I planned the architecture, made deliberate choices at each configuration step, documented the reasoning behind them, and validated the result from the end user's perspective — the same way these tasks are performed in a professional environment.

