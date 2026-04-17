# Enterprise Remote IT Support & Service Desk Operations


---

## Overview

This project records the implementation of an enterprise-style remote IT support workflow using an IT service management platform and a secure, attended remote access tool. The objective was to demonstrate how Service Desk teams provide remote assistance to end users across separate networks in a manner that is secure, consent-driven, and fully documented.

The project focuses on operational process, security controls, and documentation discipline rather than a specific end-user incident.

---

## Environment

| Component | Detail |
|---|---|
| IT Support Workstation | Host machine used to deliver remote support |
| Client Device | Separate physical machine on a different network |
| ITSM Platform | Spiceworks |
| Remote Access Tool | Zoho Assist (secure attended remote support) |
| Network Control | VPN connection active on the support workstation |
| Connectivity | Internet-connected endpoints across separate networks |
---

## Remote Support Workflow

Remote support was initiated directly from within the ITSM platform, ensuring all sessions are logged and governed by an approved system rather than ad-hoc tooling. This mirrors standard Service Desk practice, where remote access is provided only on demand and through authorised channels.
<img width="1352" height="602" alt="Screenshot from 2026-04-17 04-53-09" src="https://github.com/user-attachments/assets/21d7d5b4-0dee-4430-9957-c1aeba8f2f4c" />

---

## Secure Session Establishment

Prior to initiating the remote session
From this page, a lightweight remote support agent was downloaded and installed on the client device.

The agent installation enabled temporary communication between the client workstation and the remote support platform for the duration of the attended session. No permanent software or persistent access was configured, ensuring that remote access was limited strictly to the approved support session.
, a VPN connection was enabled on the primary workstation which changed my public IP address and virtual network location. This step allowed me to replicate a common real world scenario where IT support staff operate from a different country, branch office, or remote location while assisting users across the internet. By doing this, I validated that the remote support solution functioned correctly across different networks .
<img width="1363" height="685" alt="Screenshot from 2026-04-17 04-55-31" src="https://github.com/user-attachments/assets/30f31630-b948-4a8c-8753-303ce2180fdc" />

A one-time, HTTPS-secured session link was generated and shared with the client device to establish the attended remote connection. The use of a single-use link ensures the session cannot be replayed or reused after closure.
<img width="1366" height="601" alt="Screenshot from 2026-04-17 04-57-13" src="https://github.com/user-attachments/assets/f72d0840-fa0e-47ce-adda-4769cdf11563" />
---

## User Consent & Compliance

The remote session was configured as attended, requiring the end user to explicitly approve access before any remote control was established. The client device displayed a prompt allowing the user to accept or deny the incoming connection.
<img width="1280" height="1024" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/e1bfb8df-60e3-437a-8b00-49d90575cde3" />

Access proceeded only after the user granted approval. This control satisfies the consent, privacy, and security requirements enforced in enterprise remote support environments.
<img width="1280" height="1024" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/154e289d-273b-45d3-b5f2-fae2fb140995" />


## Active Remote Support Session

Following user approval, the attended remote session was successfully established between the support workstation and the client device, providing full remote visibility and control for the duration of the support engagement.
<img width="1366" height="768" alt="Screenshot from 2026-04-17 06-18-46" src="https://github.com/user-attachments/assets/98972d29-ac5b-435a-8bf3-1a685c853369" />
---
## Remote Session Termination, Verification & Agent Behavior

After completing the remote support activities, the attended remote session was explicitly ended from the IT support workstation. Upon termination, access to the client workstation was immediately revoked and no active remote connection remained.

The client workstation was checked to verify that the remote support session had fully ended. This confirmation ensured that no unattended or persistent access was left active after session completion, aligning with enterprise security and privacy requirements.

Although the session-based remote support agent file remained present on the client workstation, the agent was no longer running once the session ended and did not provide ongoing or background access. Any subsequent remote support session would require the user to manually launch the agent again and explicitly approve a new session.

This approach ensures that remote access is temporary, user-initiated, and controlled per session, following access control and security best practices commonly enforced in enterprise IT environments.
<img width="1280" height="1024" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/f9e4b3a2-50ac-40c0-a706-d2199de4c463" />

## Skills Demonstrated

- Secure, attended remote IT support operations
- ITSM-integrated session initiation and documentation
- VPN-based cross-network support delivery
- User consent enforcement and compliance controls
- Cloud-based remote access workflow management
- Incident record keeping and audit readiness

---

## Outcome

This lab exercise provided hands on experience with IT service management platforms, secure cloud based remote support, VPN simulated network separation, and cross network troubleshooting. It highlighted how modern IT support workflows combine multiple tools such as Spiceworks for service management and Zoho Assist for remote access to deliver effective, secure, and compliant support to users regardless of location. The exercise closely mirrors how enterprise IT support teams operate in today’s remote first and globally distributed work environments.
