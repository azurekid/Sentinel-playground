![logo](./media/securehats-200x.png)
=========
[![GitHub release](https://img.shields.io/github/release/SecureHats/Sentinel-playground.svg?style=flat-square)](https://github.com/SecureHats/Sentinel-playground/releases)
[![Maintenance](https://img.shields.io/maintenance/yes/2021.svg?style=flat-square)]()
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![Deploy To Azure](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/1-CONTRIBUTION-GUIDE/images/deploytoazure.svg?sanitize=true)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSecureHats%2FSentinel-playground%2Fmain%2FARM-Templates%2Fazuredeploy.json/createUIDefinitionUri/https%3A%2F%2Fraw.githubusercontent.com%2FSecureHats%2FSentinel-playground%2Fmain%2FARM-Templates%2FUiDefinition.json)
# Sentinel Playground

The Sentinel playground is a project to deploy an initial Azure Sentinel environment pre-provisioned with sample data. 
This to speed up the deployment for Proof of Concept and demo scenarios.

#### Prerequisites

- Azure user account with enough permissions. See table below.

The following table summarizes permissions, licenses needed and cost to enable each Data Connector:

| Provider   | Connector                                             | Custom Table                    | Parser | Tested  |
| ---------- | ----------------------------------------------------- | ------------------------------- | ------ | ------- |
| Agari      | Agari Phishing Defense and Brand Protection (Preview) | agari_apdpolicy_log_CL          |  [ ]   |   [ ]   |
| Agari      |                                                       | agari_apdtc_log_CL              |  [ ]   |   [ ]   |
| Agari      |                                                       | agari_bpalerts_log_CL           |  [ ]   |   [ ]   |
| Akamai     | Akamai Security Events (Preview)                      | SecureHats_CL                   |  [X]   |   [X]   |
| Aruba      | Aruba ClearPass (Preview)                             | SecureHats_CL                   |  [ ]   |   [X]   |
| Cisco      | Cisco ISE Event                                       | SecureHats_CL                   |  [ ]   |   [X]   |
| Cisco      | Cisco Meraki (Preview)                                | SecureHats_CL                   |  [ ]   |   [X]   |
| Cisco      | Cisco UCS (Preview)                                   | SecureHats_CL                   |  [ ]   |   [X]   |
| Cisco      | Cisco Umbrella (Preview)                              | Cisco_Umbrella_cloudfirewall_CL |  [X]   |   [X]   |
|            |                                                       | Cisco_Umbrella_dns_CL           |  [X]   |   [ ]   |
|            |                                                       | Cisco_Umbrella_ip_CL            |  [X]   |   [ ]   |
|            |                                                       | Cisco_Umbrella_proxy_CL         |  [X]   |   [ ]   |
| Qualys     | Qualys VM KnowledgeBase (Preview)                     | QualysKB_CL                     |  [X]   |   [X]   |
| Qualys     | Qualys Vulnerability Management (Preview)             | QualysHostDetection_CL          |  [X]   |   [ ]   |
| Symantec   | Broadcom Symantec DLP (Preview)                       | SecureHats_CL                   |  [X]   |   [X]   |
| Symantec   | Symantec ProxySG (Preview)                            | SecureHats_CL                   |  [X]   |   [x]   |
| Symantec   | Symantec VIP (Preview)                                | SecureHats_CL                   |  [X]   |   [x]   |


## ARM template instructions

The template performs the following tasks:

- Creates resource group (if given resource group doesn't exist yet)
- Creates Log Analytics workspace (if given workspace doesn't exist yet)
- Installs Azure Sentinel on top of the workspace (if not installed yet)
- Creates a temporary Azure Container Registry
- Creates a used assigned identity for executing the deployment scripts
- Creates a Deployment script (if given deployment script doesn't exist yet)

In order to execute the deployment scripts, the deployment template uses an [ARM deployment script](https://docs.microsoft.com/azure/azure-resource-manager/templates/deployment-script-template) which requires a [user assigned identity](https://docs.microsoft.com/azure/active-directory/managed-identities-azure-resources/overview). You will see this resource in your resource group when the deployment finishes. You can remove after depployment if desired.

It takes around **10 minutes** to before that sample data is visible.

## Supported Providers
- Aruba 
- Cisco
- Symantec

## ToDo
- Add more data providers
- Add more parsers
- Clean-up Deployment Scripts
- Enables analytics rules for selected Microsoft 1st party products 
- Enables Fusion rule and ML Behavior Analytics rules for RDP or SSH (if Security Events or Syslog data sources are selected)
- Enables Scheduled analytics rules that apply to all the enabled connectors 
