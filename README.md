# Azure-SOC
# Building a SOC + Honeynet in Azure (Live Traffic)


<img width="800" alt="image" src="https://github.com/user-attachments/assets/842a9556-05f6-48f7-95f1-2b21df484fc2" />

## Introduction

In this project, I build a mini honeynet in Azure and ingest log sources from various resources into a Log Analytics workspace, which is then used by Microsoft Sentinel to build attack maps, trigger alerts, and create incidents. I measured some security metrics in the insecure environment for 24 hours, apply some security controls to harden the environment, measure metrics for another 24 hours, then show the results below. The metrics we will show are:

- SecurityEvent (Windows Event Logs)
- Syslog (Linux Event Logs)
- SecurityAlert (Log Analytics Alerts Triggered)
- SecurityIncident (Incidents created by Sentinel)
- AzureNetworkAnalytics_CL (Malicious Flows allowed into our honeynet)

## Architecture Before Hardening / Security Controls

<img width="800" alt="image" src="https://github.com/user-attachments/assets/af0c7977-e371-457e-bcf5-b972a33453d4" />

## Architecture After Hardening / Security Controls


<img width="800" alt="image" src="https://github.com/user-attachments/assets/27d670af-7c16-4135-b26a-f0f54835160d" />

The architecture of the mini honeynet in Azure consists of the following components:

- Virtual Network (VNet)
- Network Security Group (NSG)
- Virtual Machines (2 windows, 1 linux)
- Log Analytics Workspace
- Azure Key Vault
- Azure Storage Account
- Microsoft Sentinel

For the "BEFORE" metrics, all resources were originally deployed, exposed to the internet. The Virtual Machines had both their Network Security Groups and built-in firewalls wide open, and all other resources are deployed with public endpoints visible to the Internet; aka, no use for Private Endpoints.

For the "AFTER" metrics, Network Security Groups were hardened by blocking ALL traffic with the exception of my admin workstation, and all other resources were protected by their built-in firewalls as well as Private Endpoint

## Attack Maps Before Hardening / Security Controls

<img width="800" alt="image" src="https://github.com/user-attachments/assets/3a01f8d8-8847-4854-9e46-43980dfdce51" />

<img width="800" alt="image" src="https://github.com/user-attachments/assets/37fdd5f8-49bf-4ab9-a789-d1b9160b0f46" />

<img width="800" alt="image" src="https://github.com/user-attachments/assets/948c1332-bb2b-4878-8ecb-d9a23c6629cc" />


## Metrics Before Hardening / Security Controls

The following table shows the metrics we measured in our insecure environment for 24 hours:
Start Time 2025-01-07 19:00:29
Stop Time 2025-01-08 19:00:29

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 21093
| Syslog                   | 18831
| SecurityAlert            | 1
| SecurityIncident         | 238
| AzureNetworkAnalytics_CL | 1948

## Attack Maps Before Hardening / Security Controls

```All map queries actually returned no results due to no instances of malicious activity for the 24 hour period after hardening.```

## Metrics After Hardening / Security Controls

The following table shows the metrics we measured in our environment for another 24 hours, but after we have applied security controls:
Start Time 2025-1-12 03:00:32
Stop Time	2025-1-13 03:00:32

| Metric                   | Count
| ------------------------ | -----
| SecurityEvent            | 379
| Syslog                   | 13
| SecurityAlert            | 0
| SecurityIncident         | 0
| AzureNetworkAnalytics_CL | 0

## Conclusion

In this project, a mini honeynet was constructed in Microsoft Azure and log sources were integrated into a Log Analytics workspace. Microsoft Sentinel was employed to trigger alerts and create incidents based on the ingested logs. Additionally, metrics were measured in the insecure environment before security controls were applied, and then again after implementing security measures. It is noteworthy that the number of security events and incidents were drastically reduced after the security controls were applied, demonstrating their effectiveness.

It is worth noting that if the resources within the network were heavily utilized by regular users, it is likely that more security events and alerts may have been generated within the 24-hour period following the implementation of the security controls.
