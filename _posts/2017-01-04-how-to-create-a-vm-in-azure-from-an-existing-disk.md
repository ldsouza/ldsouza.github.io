---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: How to create a VM in Azure from an existing Disk
category: Azure
tags:
  - Azure
  - Cloud
  - Powershell
---

In this blog post, I will show you how to create a virtual machine in Azure from an existing disk in an Azure storage account. This Azure RM PowerShell script is useful when you want to move your on-premises virtual machines to Azure. Before you can run this script, you would have to first copy your on-premises disks in vhd format to an Azure Storage Account.
![Image]({{ site.url }}/images/blog/generic/azure.jpg)

In this example we will be using Azure Resource Manager to create a new virtual machine.

Log in to your Azure Account using the following command.

```javascript
Login-AzureRmAccount
```

![Image]({{ site.url }}/images/blog/how-to-create-vm-azure/1.JPG)

Copy the path of the existing Virtual Machine OS disk from the storage account.

```javascript
$destinationVhd = "https://azure.blob.core.windows.net/vhds/dev.vhd"
```
Define the Resource Group, Virtual Network and Location for the new virtual machine.

```javascript
$rgName = "Azure-RG"
$virtualNetworkName = "Azure-VNetwork"
$locationName = "East US"
```

Create a Network Interface with a public IP Address to access the new VM.

```javascript
$virtualNetwork = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $virtualNetworkName
$publicIp = New-AzureRmPublicIpAddress -Name "dev11" -ResourceGroupName $rgName -Location 
$locationName -AllocationMethod Dynamic
$networkInterface = New-AzureRmNetworkInterface -ResourceGroupName $rgName -Name "dev11" -
Location $locationName -SubnetId $virtualNetwork.Subnets[1].Id -PublicIpAddressId $publicIp.Id
```

Set the virtual machine size by looking up the available virtual machine sizes for the location specified earlier.

```javascript
Get-AzureRmVMSize $locationName | Out-GridView
```

We are now ready to create the VM.

```javascript
$vmConfig = New-AzureRmVMConfig -VMName "DEV" -VMSize "Standard_DS1"
$vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name "DEV" -VhdUri $destinationVhd -CreateOption 
Attach -Windows
$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $networkInterface.Id
$vm = New-AzureRmVM -VM $vmConfig -Location $locationName -ResourceGroupName $rgName
```

#### How to attach an existing data disk to a VM

```javascript
Login-AzureRmAccount
#attach existing datadisks to VM
$rgName = "Azure-RG"
$vmname = "DEV-VM"
$DataDiskUri = "https://azure.blob.core.windows.net/vhds/DEV-VM-disk-1-20161226192045.vhd"
$vmConfig=Get-AzurermVM -ResourceGroupName $rgname -Name $vmname
Add-AzureRMVMDataDisk -Name "DEV-VM-Data03" -VM $vmConfig -VhdUri $DataDiskUri -LUN 1 -Caching None -CreateOption Attach -DiskSizeInGB 1023
Update-AzureRmVM -ResourceGroupName $rgname -VM $vmConfig
```

Another scenario, where this script could be handy, is if you want to move an existing virtual machine in Azure to a different network. Azure does not let you move a VM to another network, so we have a to delete the existing VM and re-create it using its disks.



