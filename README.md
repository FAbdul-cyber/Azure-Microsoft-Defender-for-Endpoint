
# Azure Microsoft Defender for Endpoint

## Project Overview

This project explores cloud security, identity and access management, endpoint protection, and security operations within a Microsoft Azure environment.

So far, I have gained hands-on experience in creating and managing users in Microsoft Entra ID, implementing Role-Based Access Control (RBAC), and enforcing the Principle of Least Privilege (PoLP).

I have also utilized Azure Log Analytics and Kusto Query Language (KQL) to identify an IP address and leveraged VirusTotal to investigate its reputation and potential malicious activity.

The project will expand to include endpoint detection and response, controlled attack simulations, security alert investigations, authentication activity analysis, and remote endpoint investigations using Microsoft Defender for Endpoint.

---

## Skills Demonstrated

- Identity and Access Management (IAM)
- Microsoft Entra ID
- Role-Based Access Control (RBAC)
- Principle of Least Privilege (PoLP)
- User Provisioning and Access Management
- Kusto Query Language (KQL)
- Azure Log Analytics
- Open-Source Threat Intelligence (OSINT)
- IP Address Reputation Analysis
- Indicator of Compromise (IOC) Investigation

---

## What I Learned

Through this project, I have developed a practical understanding of identity security, access management, and introductory threat investigation within a Microsoft Azure environment.

I learned how to create and manage user accounts in Microsoft Entra ID, assign role-based permissions, and apply the Principle of Least Privilege to minimize unnecessary access to cloud resources.

I also gained experience using Kusto Query Language (KQL) within Azure Log Analytics to identify an IP address and investigate its reputation using VirusTotal.

This investigation strengthened my understanding of how threat intelligence can support security analysts in identifying potentially malicious activity.

---

## Technologies Used

- Microsoft Azure
- Microsoft Entra ID
- Azure Role-Based Access Control (RBAC)
- Azure Log Analytics
- Kusto Query Language (KQL)
- VirusTotal

---

## 1. Identity and Access Management

Created and configured test employee accounts in Microsoft Entra ID to simulate an organizational environment with users from different departments.

The following accounts were provisioned:

- Fahima Abdul — Developer
- Jennifer Halvey — Human Resources (HR)
- Kattie Hoven — Security

The objective was to establish a foundation for identity management, role-based access control, and the implementation of the Principle of Least Privilege.


![Microsoft Entra ID User Accounts](screenshots/01-entra-id-users.png)

*Figure 1: Test employee accounts provisioned in Microsoft Entra ID.*

---

### Role-Based Access Control (RBAC) and Principle of Least Privilege

Implemented Azure Role-Based Access Control (RBAC) within the Cyberproject1 resource group to manage employee access based on their organizational responsibilities.


### Role-Based Access Control (RBAC) and Least Privilege

Assigned Azure RBAC roles within the Cyberproject1 resource group based on each employee's responsibilities.

- Fahima Abdul — Contributor
- Jennifer Halvey — Reader
- Kattie Hoven — Security Reader

Restricted permissions to the resource group scope to support the Principle of Least Privilege.

![Azure RBAC Role Assignments](screenshots/02-rbac-role-assignments.png)

*Figure 2: Azure RBAC role assignments.*

---
## 2. Network Traffic Analysis and Threat Intelligence

Conducted a network traffic investigation using Azure Log Analytics, Kusto Query Language (KQL), and VirusTotal to identify suspicious inbound SSH traffic and assess IP address reputation.

### Log Analytics Workspace

Configured an Azure Log Analytics workspace for querying and analyzing network traffic data.

![Log Analytics Workspace](screenshots/01-log-analytics-workspace.png)

*Figure 3: Azure Log Analytics workspace.*

### SSH Traffic Investigation Using KQL

Used KQL to filter network traffic targeting SSH (port 22) and identify public source IP addresses.

![SSH Traffic Investigation](screenshots/02-ssh-traffic-investigation.png)

*Figure 4: KQL query filtering SSH traffic.*

Aggregated network flows by source IP address to identify allowed and denied traffic.

![Source IP Analysis](screenshots/03-source-ip-analysis.png)

*Figure 5: Analysis of network flows by source IP address.*

### Threat Intelligence Investigation

Investigated the suspicious IP address 193.32.162.15 using VirusTotal. The IP address was flagged as malicious by 15 out of 92 security vendors and associated with SSH brute-force activity and network scanning in threat intelligence reports.

![VirusTotal Threat Intelligence](screenshots/04-virustotal-threat-intelligence.png)

*Figure 6: IP reputation investigation using VirusTotal.*

### Network Security Group (NSG) Review

Reviewed inbound NSG rules to understand existing network access controls and traffic restrictions.

![NSG Inbound Rules](screenshots/05-nsg-inbound-rules.png)

*Figure 7: Azure Network Security Group rules.*

### Investigation Findings

- Identified suspicious inbound traffic targeting SSH.
- Observed denied network flows from suspicious source IP addresses.
- Correlated network traffic findings with external threat intelligence.
- Reviewed existing network security controls.

No successful SSH connection or system compromise was established by this investigation.

---

## 3. Simulated Brute-Force Attack and Failed Authentication Analysis

Simulated a brute-force attack against an Azure Windows Server VM by attempting multiple RDP logins using invalid credentials in a controlled lab environment.

### Failed Authentication Investigation

Queried Windows Security Events using KQL to identify failed authentication attempts (Event ID 4625).

![Failed Logon Events](screenshots/08-failed-logon-event-4625.png)

*Figure 8: Windows failed logon events identified using KQL.*

### Threshold-Based Threat Detection

Developed a KQL query to identify source IP addresses associated with three or more failed authentication events within a 60-minute period.

![Brute Force Detection](screenshots/09-brute-force-detection-query.png)

*Figure 9: KQL detection query identifying 10 failed logon events from a single source IP address.*

### Investigation Findings

- Successfully generated and collected failed authentication events.
- Identified 10 failed logon events from a single source IP address.
- Validated threshold-based detection logic using KQL.
- Observed Windows authentication rejecting invalid credentials.

---

## 4. Microsoft Defender for Endpoint Onboarding and Verification

Onboarded an Azure Windows Server VM to Microsoft Defender for Endpoint (MDE) to establish endpoint monitoring capabilities.

### Endpoint Onboarding

Executed the Microsoft Defender for Endpoint local onboarding script with administrative privileges.

![Successful MDE Onboarding](screenshots/10-successful-mde-onboarding.png)

*Figure 10: Successful execution of the MDE onboarding script.*

### Sensor and Onboarding Verification

Used PowerShell to verify the Defender for Endpoint sensor service and confirm the local onboarding status.

![MDE Sensor Verification](screenshots/11-mde-sensor-and-onboarding-verification.png)

*Figure 11: Verification of the running Sense service and OnboardingState.*

### Results

- Successfully executed the endpoint onboarding script.
- Verified that the MDE sensor service (Sense) was running.
- Confirmed local onboarding status through the Windows Registry (OnboardingState = 1).

---

## 5. Simulated PowerShell Attack and Endpoint Incident Response

Conducted an authorized PowerShell attack simulation using a Microsoft-provided training script to evaluate Microsoft Defender for Endpoint's threat detection and prevention capabilities.

### Attack Simulation and Prevention

Executed an obfuscated PowerShell script in a controlled lab environment. Microsoft Defender detected malicious script content and blocked its execution.

![PowerShell Attack Blocked](screenshots/12-powershell-attack-blocked.png)

*Figure 12: Malicious PowerShell script execution blocked by endpoint protection.*

### Attack Technique Analysis

Reviewed the PowerShell attack script to understand the techniques behind the simulated malicious activity.

The script demonstrated:

- Base64 decoding using `FromBase64String`.
- XOR-based deobfuscation using the `-bxor` operator.
- Reconstruction of decoded content in memory.
- Attempted dynamic execution using `Invoke-Expression`.

These techniques can be used by threat actors to conceal malicious payloads and evade basic security inspection.

Analyzing the script helped me understand how threat actors can abuse legitimate PowerShell functionality to execute concealed commands.

### Alert and Incident Investigation

Investigated the generated Empire tool detection in the Microsoft Defender portal, reviewing associated alerts, process details, evidence and the process tree.

![Empire Alert Analysis](screenshots/13-mde-empire-alert-analysis.png)

*Figure 13: Microsoft Defender evidence showing malicious PowerShell activity and blocked status.*

### PowerShell Log Analysis Using KQL

Queried Windows PowerShell operational logs in Azure Log Analytics using Event ID 4103 to verify the collection of PowerShell module logging events.

![PowerShell Event Analysis](screenshots/14-powershell-event-4103.png)

*Figure 14: PowerShell operational telemetry retrieved using KQL.*

### Incident Response and Containment

Practiced endpoint containment by isolating the affected virtual machine through Microsoft Defender for Endpoint. Subsequently released the device from isolation after completing the controlled simulation.

### Investigation Findings

- Validated endpoint threat detection and prevention capabilities.
- Analyzed PowerShell script obfuscation and execution techniques.
- Investigated malicious PowerShell activity and associated alert evidence.
- Reviewed process information and the process tree.
- Verified PowerShell operational log collection using KQL.
- Practiced endpoint isolation and release from isolation.

---

## 6. Microsoft Defender Live Response and Threat Remediation

Used Microsoft Defender for Endpoint's Live Response capability to remotely remediate the PowerShell attack script from the simulated security incident.

### Remote File Remediation

Established a Live Response session with the endpoint and executed the `remediate file` command to quarantine the malicious PowerShell script (`AttackScript.ps1`).

### Remediation Verification

Reviewed the remediation output to confirm that the file was successfully quarantined and the operation completed without reported errors.

Used the `dir` command to verify that the script was no longer present in its original directory.

![Live Response File Remediation](screenshots/15-live-response-file-remediation.png)

*Figure 15: Successful file quarantine and remediation verification using Microsoft Defender Live Response.*

### Investigation Findings

- Established a remote Live Response session.
- Performed manual threat remediation.
- Successfully quarantined the simulated malicious PowerShell script.
- Verified remediation status and removal from the original file location.

---


---

---
