
# Enterprise Patch Management & Endpoint Enrollment Using Action1

## Overview

This document describes the process followed to deploy and enroll endpoints into the **Action1 patch management platform**. The purpose of this documentation is to record a clear, professional, and repeatable deployment process that can be referenced for future endpoint onboarding, validation, or audit purposes within an enterprise-style IT environment.

The deployment focuses specifically on **agent installation, endpoint registration, and verification**, forming the foundation for centralized patch management and endpoint visibility.

---

## Environment

- Action1 cloud-based patch management platform  
- Windows Server (domain server)  
- Windows workstation  
- Internet-connected endpoints  
- Web browser for administrative access  

---

## Step 1: Accessing the Action1 Management Console

I began by logging into the **Action1 web-based management console** using assigned administrative credentials. As Action1 is a **cloud-hosted platform**, no on-premises management server was required to manage or monitor enrolled endpoints. All administration was performed directly through the web interface.

---

## Step 2: Downloading the Action1 Agent

From the Action1 dashboard, I navigated to the section used for adding new endpoints and downloaded the **Action1 agent installer**. The agent is required to establish communication between each endpoint and the Action1 management platform.
<img width="1353" height="599" alt="Screenshot from 2026-04-16 01-39-45" src="https://github.com/user-attachments/assets/6e3b6fed-6b8a-4287-8da3-158e90a4f957" />

---

## Step 3: Installing the Agent on Endpoints

After downloading the installer, I deployed the Action1 agent on both a **server** and a **workstation**.  
Each device required an active internet connection to complete installation, allowing the agent to authenticate, register, and synchronize with the Action1 cloud platform during setup.

The installation process completed successfully on both endpoints without requiring additional configuration.
<img width="1356" height="618" alt="Screenshot from 2026-04-16 01-42-53" src="https://github.com/user-attachments/assets/eacddb27-f83a-4b75-a6db-757b52c2f7cd" />
<img width="1356" height="618" alt="Screenshot from 2026-04-16 02-01-28" src="https://github.com/user-attachments/assets/5c88d8bf-8b79-48c7-894a-8ee91d58dfd3" />

---

## Step 4: Endpoint Registration and Verification

Once installation was completed, both the server and workstation automatically registered with the Action1 platform. I verified successful enrollment by confirming that each endpoint appeared in the **Endpoints** section of the Action1 console.
<img width="1360" height="606" alt="Screenshot from 2026-04-16 15-46-48" src="https://github.com/user-attachments/assets/e37c1c8e-1cb3-42e2-9119-02b54d773e9c" />

The visibility of both devices in the dashboard confirmed that:
- The agent was installed correctly  
- The endpoints were registered successfully  
- Communication with the Action1 platform was active  
<img width="1360" height="606" alt="image" src="https://github.com/user-attachments/assets/f608a136-bcc7-40d5-900d-2f0d35a96feb" />

---

## Step 5: Post-Installation Capabilities

After enrollment, the endpoints became available for centralized management through the Action1 platform. This provides access to platform-supported capabilities such as:

- Operating system patch management  
- Third-party application patching  
- Vulnerability detection  
- Remote command execution  
- Software deployment  
- Compliance and reporting functions  

These capabilities form the basis for maintaining endpoint security and patch consistency across the environment.

---

## Conclusion

The successful installation and enrollment of the Action1 agent on both a server and a workstation demonstrates the efficiency and simplicity of the platform’s deployment model. This documented process can be repeated to onboard additional endpoints consistently, supporting centralized patch management and improved visibility across enterprise environments.

---
