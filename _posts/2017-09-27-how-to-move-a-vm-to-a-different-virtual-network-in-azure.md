---
layout: post
published: false
categories:
  - personal
mathjax: false
featured: false
comments: false
title: How to move a VM to a different virtual network in Azure
---

We often encounter scenarios where we have to move development workloads to a production network. In an on-premise environment, moving virtual machines to a different virtual network is a breeze, but it has not always been straightforward in Azure.

One of the methods to moving a virtual machine in Azure, is deleting the existing VM, creating a new VM in the new network and then attaching the existing disks. 

In this blog post, I will show you how to moving a vm to a different virtal network using Azure Recovery Services Vault.

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/5.JPG)

First we need to setup Azure , follow the five steps below -

### 1) Create a Group called 'AAD DC Administrators' in Azure AD.

The members of this group are granted administrative privileges on machines joined to the Azure AD Domain. Set the group type of this group to 'Security'.

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/1.JPG)

### 2) Create a classic Virtual Network

Azure AD Domain Services is not supported in Azure Resource Manager, so we have to create a virtual network and subnet in the Azure classic portal to enable Azure AD Domain Services. 

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/2.JPG)

### 3) Enable Azure AD Domain Services in the Classic Portal

Click Active Directory in the Classic Portal and select the 'Configure' tab.
Scroll to Domain Services and change the setting from 'No' to 'Yes' and select a DNS name of this managed domain service and the virtual network we created earlier.

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/3.JPG)

### 4) Set the DNS server of the Virtual network

After enabling Domain Services, two IP Addresses will be displayed under Domain Services. Note this down and add this as a DNS Server in the virtual network configuration under Networks.

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/4.JPG)

### 5) Enable synchronization of credential hashes to AAD

Run the following PowerShell script after replacing the relevant connector names below. To find the connector names, open Synchronization Services on the AD Connect Server and click the connectors tab.

AD CONNECTOR NAME is the connector of Type 'Active Directory Domain Services'.

AAD Connector Name is the connector of Type 'Windows Azure Active Directory (Microsoft).

```javascript
$adConnector = “<CASE SENSITIVE AD CONNECTOR NAME>”
$aadConnector = “<CASE SENSITIVE AAD CONNECTOR NAME>”
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter “Microsoft.Synchronize.ForceFullPasswordSync”, String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

Once this is complete, users can sign into computers joined to the managed domain using their Azure AD credentials.

### Challenges

Since Azure AD Domain Services is not supported in Azure Resource Manager yet, a big challenge is setting this up with Azure Resource Manager (ARM) virtual machines. To accomplish this, we have to set a VPN connection between the Classic Network in which Azure AD Domain Services is enabled and the Azure RM Network.
