Table of Contents

[Introduction](#introduction)

[Planning](#_Toc218843267)

[Deployment Scenario](#_Toc218843268)

[Pre-requisites](#_Toc218843269)

[Subscriptions](#_Toc218843270)

[Identities](#_Toc218843271)

[Azure Entra ID](#_Toc218843272)

[Defender Email Account (terraform only)](#_Toc218843273)

[Service Accounts](#_Toc218843274)

[Bootstrap](#_Toc218843275)

[Version Control Systems](#_Toc218843276)

[DevOps Networking](#_Toc218843277)

[Naming Conventions](#_Toc218843278)

[Platform Networking](#_Toc218843279)

[Deployment Scenarios](#deployment-scenarios)

[Hub and Spoke](#_Toc218843281)

[VWAN](#_Toc218843282)

[IP Addresses](#_Toc218843283)

[Options](#_Toc218843284)

[Azure Policy](#_Toc218843285)

[Run](#_Toc218843286)

[Variables](#_Toc218843287)

[Example](#_Toc218843288)

[PowerShell](#_Toc218843289)

[Step 1](#_Toc218843290)

[Step 2](#_Toc218843291)

[Step 3](#_Toc218843292)

[Bicep](#_Toc218843293)

[Terraform](#_Toc218843294)

# Introduction

This document serves as a comprehensive planning and deployment guide for Azure Platform Landing Zone environments, covering deployment scenarios such as management groups, networking (Hub and Spoke, Virtual WAN), and security options including Azure Firewall and Network Virtual Appliances. It outlines prerequisites like subscription details and identity management, version control and infrastructure-as-code tools, DevOps networking configurations, naming conventions, platform networking scenarios, IP addressing, Azure policy enforcement, and necessary software installations for deployment such as PowerShell, Azure CLI, and Git.

# Planning

## Deployment Scenario

| **Setting**                                                                                                                                                                                  | **Value** |
|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------|
| [Management Groups, Policy and Management Resources Only](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/management-only/) | Yes       |
| Hub and Spoke Networking                                                                                                                                                                     | No        |
| VWan Networking                                                                                                                                                                              | Yes       |
| Single Region                                                                                                                                                                                | No        |
| Multi-Region                                                                                                                                                                                 | Yes       |
| Azure Firewall                                                                                                                                                                               | Yes       |
| Network Virtual Appliance                                                                                                                                                                    | No        |

# Pre-requisites

## Subscriptions

|                  | **Subscription Name** | **Subscription ID**                  | **Subscription Provider** |
|------------------|-----------------------|--------------------------------------|---------------------------|
| **Management**   | Management            | 4ae4d0dd-086f-45ee-a6cb-887037a46934 | PAYG                      |
| **Connectivity** | Connectivity          | e0a9e44b-88a6-4bb1-936f-ace5f92124ce | PAYG                      |
| **Identity**     | Identity              | 8abb7f02-1984-4dc2-a4d3-fd02e04be430 | PAYG                      |
| **Security**     | Security              | ca0af382-499c-4a25-823a-6a0e8f89874a | PAYG                      |
| **Boot Strap**   | Management            | 4ae4d0dd-086f-45ee-a6cb-887037a46934 | PAYG                      |

**Note:**

Subscription vending only works with the one of the following Subscription Providers –

-   Enterprise Agreement (EA)
-   Microsoft Customer Agreement (MCA)
-   Microsoft Partner Agreement (MPA)

## Identities

### Azure Entra ID

| Tenant ID | 7d6abfdd-038d-40a5-aee9-5474ed1ac8d5 |
|-----------|--------------------------------------|

### Defender Email Account (terraform only)

| Email Address | [Ashley.rutland@rutlandblog.com](mailto:Ashley.rutland@rutlandblog.com) |
|---------------|-------------------------------------------------------------------------|

### Service Accounts

|   |   |
|---|---|
|   |   |

# Bootstrap

## Version Control Systems

| **VCS Version** | **IAC Version** |
|-----------------|-----------------|
| Azure DevOps    | Terraform       |

**Note:**

**VCS Versions:** Azure Devops, Github, Local, Other

**IAC Version:** Terraform, Bicep

### DevOps Networking

Once you’ve decided on what VCS and IaC you want to use you then need to think about the agents for deploying your IaC.

|                                                          | **Azure DevOps**                   | **GitHub**                      |
|----------------------------------------------------------|------------------------------------|---------------------------------|
| Private networking with self-hosted agents / runners     | use_private_networking = true      | use_private_networking = true   |
|                                                          | use_self_hosted_agents = true      | use_self_hosted_runners = true  |
| Public networking with self-hosted agents / runners      | use_private_networking = false     | use_private_networking = false  |
|                                                          | use_self_hosted_agents = true      | use_self_hosted_runners = true  |
| Public networking with Microsoft-hosted agents / runners | **use_private_networking = false** | use_private_networking = fals   |
|                                                          | **use_self_hosted_agents = false** | use_self_hosted_runners = false |

**Note: Highlight the option to be used**

## Naming Conventions

| **Name**            | **Value** |
|---------------------|-----------|
| 3 Letter Prefix     | ACR       |
| Primary Region      | UKS       |
| Secondary/DR Region | UKW       |
|                     |           |

## Platform Networking

### Deployment Scenarios

|               | **Multi/Single-Region** | **Azure Firewall** | **NVA** |
|---------------|-------------------------|--------------------|---------|
| Hub and Spoke | Multi/Single            | Yes/No             | Yes/No  |
| Virtual WAN   | Multi                   | Yes                | No      |

1.  [Multi-Region Hub and Spoke Virtual Network with Azure Firewall](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/multi-region-hub-and-spoke-vnet-with-azure-firewall/)
2.  [Multi-Region Virtual WAN with Azure Firewall](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/multi-region-virtual-wan-with-azure-firewall/)
3.  [Multi-Region Hub and Spoke Virtual Network with Network Virtual Appliance (NVA)](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/multi-region-hub-and-spoke-vnet-with-nva/)
4.  [Multi-Region Virtual WAN with Network Virtual Appliance (NVA)](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/multi-region-virtual-wan-with-nva/)
5.  [Management Groups, Policy and Management Resources Only](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/management-only/)
6.  [Single-Region Hub and Spoke Virtual Network with Azure Firewall](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/single-region-hub-and-spoke-vnet-with-azure-firewall/)
7.  [Single-Region Virtual WAN with Azure Firewall](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/single-region-virtual-wan-with-azure-firewall/)
8.  [Single-Region Hub and Spoke Virtual Network with Network Virtual Appliance (NVA)](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/single-region-hub-and-spoke-vnet-with-nva/)
9.  [Single-Region Virtual WAN with Network Virtual Appliance (NVA)](https://azure.github.io/Azure-Landing-Zones/accelerator/startermodules/terraform-platform-landing-zone/scenarios/single-region-virtual-wan-with-nva/)

### Hub and Spoke

### VWAN

### IP Addresses

| **Setting** | **CIDR Range** |
|-------------|----------------|
| Hub VNet    |                |
|             |                |

## Options

| **Setting**                                | **Value** |
|--------------------------------------------|-----------|
| DDOS                                       | Yes       |
| Bastion                                    | Yes       |
| Private DNS Zones and Private DNS Resolver | Yes       |
| Virtual Network Gateways                   | Yes       |
| Regions                                    | UKS/UKW   |
| Azure Monitoring Agent                     | Yes       |
| Azure Monitoring Baseline Alerts           | Yes       |
| Defender Plans                             | Yes       |
| Zero Trust Networking                      |           |
| Sovereign Landing Zones                    |           |

### Azure Policy

| **Setting**               | **Value** |
|---------------------------|-----------|
| Policy Enforcement        | Yes/No    |
| Remove Policy Assignment  |           |
| Custom Policy Assignments |           |

# Run

The following must be installed prior to deployment:

-   PowerShell 7.4 (or newer): [Follow the instructions for your operating system](https://learn.microsoft.com/powershell/scripting/install/installing-powershell)
-   Azure CLI 2.55.0 (or newer): [Follow the instructions for your operating system](https://learn.microsoft.com/cli/azure/install-azure-cli)
-   Git (any supported version): [Follow the instructions for your operating system](https://git-scm.com/downloads).

For detailed instructions click here: [Phase 2 - Bootstrap \| Azure landing zone Documentation](https://azure.github.io/Azure-Landing-Zones/accelerator/2_bootstrap/)

## Variables

\$iacType = "terraform" \# [Must be one of: "bicep" (Recommended), "terraform" (Recommended), or "bicep-classic" (Not Recommended)](#version-control-systems)

\$versionControl = "github" [\# Must be one of: "azure-devops", "github", "local"](#version-control-systems)

\$scenarioNumber = 1 [\# Must be a number between 1 and 9 for Terraform only. Ignored for Bicep.](#_Scenarios_–_Deployment)

\$targetFolderPath = "\~/accelerator" \# Choose your target folder for the cached files

### Example

1\. \$iacType = "terraform"

***

2\. \$versionControl = "azure-devops"

***

3\. \$scenarioNumber = 2

***

4\. \$targetFolderPath = "C:\\accelerator\\AzureDevOps\\ scenario_2"

***

## PowerShell

### Step 1

Needs PowerShell to be run as Administrator

1\. \$alzModule = Get-InstalledPSResource -Name ALZ 2\>\$null

***

2\. if (-not \$alzModule) {

***

3\. Install-PSResource -Name ALZ

***

4\. } else {

***

5\. Update-PSResource -Name ALZ

***

6\. }

***

### Step 2

1\. New-AcceleratorFolderStructure \`

***

2\. -iacType \$iacType \`

***

3\. -versionControl \$versionControl \`

***

4\. -scenarioNumber \$scenarioNumber \`

***

5\. -targetFolderPath \$targetFolderPath

***

### Step 3

1\. code (Resolve-Path "\$targetFolderPath/config").Path

***

### Step 4

Update Inputs.yaml

#### Bicep

#### Terraform

Inputs.yaml (update all text in Green)

1\. ---

***

2\. \# Required Inputs

***

3.

***

4\. \# This section contains the required inputs to bootstrap the Platform Landing Zone

***

5\. \# For more detail on these inputs, visit: https://aka.ms/alz/acc/phase0

***

6.

***

7\. \# For advanced configuration options, any variable available in the bootstrap module can be set in this file

***

8\. \# You can find them here: https://aka.ms/alz/acc/bootstrap/azuredevops/variables

***

9.

***

10\. \#\# Decision 4: Bootstrap Resource Azure Region

***

11\. bootstrap_location: "\<region-1\>"

***

12.

***

13\. \#\# Decision 6: Parent Management Group

***

14\. root_parent_management_group_id: "" \# Leave empty to use Tenant Root Group

***

15.

***

16\. \#\# Decision 7: Platform Subscriptions

***

17\. subscription_ids:

***

18\. management: "\<management-subscription-id\>"

***

19\. identity: "\<identity-subscription-id\>"

***

20\. connectivity: "\<connectivity-subscription-id\>"

***

21\. security: "\<security-subscription-id\>"

***

22.

***

23\. \#\# Decision 8: Bootstrap Resource Subscription

***

24\. bootstrap_subscription_id: "" \# Leave empty to use the subscription connected to Azure CLI

***

25.

***

26\. \#\# Decision 9: Bootstrap Resource Naming.

***

27\. \# Default names can be found here: https://aka.ms/alz/acc/bootstrap/azuredevops/resourcenames

***

28\. \# For fully custom naming see the FAQ here: https://aka.ms/alz/acc/faq/bootstrap

***

29\. service_name: "alz"

***

30\. environment_name: "mgmt"

***

31\. postfix_number: 1

***

32.

***

33\. \#\# Decision 10: Bootstrap Networking and Agents

***

34\. use_self_hosted_agents: true

***

35\. use_private_networking: true

***

36.

***

37\. \#\# Decision 11: Version Control System Settings

***

38\. azure_devops_personal_access_token: "\<token-1\>" \# Can also be supplied via environment variable TF_VAR_azure_devops_personal_access_token

***

39\. azure_devops_agents_personal_access_token: "\<token-2\>" \# Can also be supplied via environment variable TF_VAR_azure_devops_agents_personal_access_token

***

40\. azure_devops_organization_name: "\<azure-devops-organization\>"

***

41\. azure_devops_project_name: "\<azure-devops-project-name\>"

***

42\. apply_approvers: ["\<email-address\>"]

***

43.

***

44\. \# Basic Inputs (Do not modify)

***

45\. iac_type: "terraform"

***

46\. bootstrap_module_name: "alz_azuredevops"

***

47\. starter_module_name: "platform_landing_zone"

***

48.

***

Step 5

1\. az login --tenant "\<tenant-id\>" --use-device-code

***

2\. az account set --subscription "\<bootstrap-subscription-id\>"

***
