---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: How to create a VM in Azure from an existing Disk
---

In this blog post, I will show you how to create a virtual machine in Azure from an existing disk in a storage account. This Azure RM powershell script is useful when you want to move your on-premises virtual machines to Azure. You would have to first copy your on-premises disks in vhd format to an Azure Storage Account, before you can run this script.

![Image]({{ site.url }}/images/blog/generic/azure.jpg)

```javascript
Login-AzureRmAccount
$destinationVhd = "https://azure.blob.core.windows.net/vhds/dev.vhd"
$rgName = "Azure-RG"
$virtualNetworkName = "Azure-VNetwork"
$locationName = "East US"
$virtualNetwork = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $virtualNetworkName
$publicIp = New-AzureRmPublicIpAddress -Name "dev11" -ResourceGroupName $rgName -Location 
$locationName -AllocationMethod Dynamic
$networkInterface = New-AzureRmNetworkInterface -ResourceGroupName $rgName -Name "dev11" -
Location $locationName -SubnetId $virtualNetwork.Subnets[1].Id -PublicIpAddressId $publicIp.Id
$vmConfig = New-AzureRmVMConfig -VMName "DEV" -VMSize "Standard_DS1"
$vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name "DEV" -VhdUri $destinationVhd -CreateOption 
Attach -Windows
$vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $networkInterface.Id
$vm = New-AzureRmVM -VM $vmConfig -Location $locationName -ResourceGroupName $rgName
```

How to attach an existing data disk to a VM

```javascript
Login-AzureRmAccount
#attach existing datadisks to VM
$rgName = "Azure-CPI"
$vmname = "DEV-CRM"
$DataDiskUri = "https://azurecpidisks280.blob.core.windows.net/vhds/DEV-CRM-disk-1-20161226192045.vhd"
$vmConfig=Get-AzurermVM -ResourceGroupName $rgname -Name $vmname
Add-AzureRMVMDataDisk -Name "DEV-CRM-Data03" -VM $vmConfig -VhdUri $DataDiskUri -LUN 1 -Caching None -CreateOption Attach -DiskSizeInGB 1023
Update-AzureRmVM -ResourceGroupName $rgname -VM $vmConfig
```

Another scenario is if you want to move a existing virtual machine in Azure to a different network. Azure does not let you move a vm to another network, so we have a to delete the existing VM and re-create it using its disks.


 
