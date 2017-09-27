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

Here is a step-by-step guide -

### 1) Create a Recovery Services Vault in Azure

Enter the name of the Vault, select the subscription, Resource group and region.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/0.JPG)

Once the recovery services vault is created, create a new backup

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/1.JPG)

### 2) Configure the Virtual Machine Backup

Create a New Backup Goal and Backup Policy. Select the Backup Frequency and Retention Range. You can create a new policy to set this backup to not re-occur.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/2.JPG)

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/3.JPG)

Select the Virtual Machine to Backup. This is the VM in our old network.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/4.JPG)

### 3) Backup the Virtual Machine from the old network

Once the configuration is complete, click Backup Now to begin the backup of the VM. You should recieve a popup alert in Azure once the backup is complete.

![Image]({{ site.url }}/images/blog/move-azure-vm-vnet/5.JPG)

### 4) Restore the Virtual Machine to the new network

After Backup is complete, select the 

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
