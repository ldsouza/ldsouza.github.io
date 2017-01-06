---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: How to create a VM in Azure from an existing Disk
---

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

<code>
Login-AzureRmAccount
#attach existing datadisks to VM
$rgName = "Azure-CPI"
$vmname = "DEV-CRM"
$DataDiskUri = "https://azurecpidisks280.blob.core.windows.net/vhds/DEV-CRM-disk-1-20161226192045.vhd"
$vmConfig=Get-AzurermVM -ResourceGroupName $rgname -Name $vmname
 
Add-AzureRMVMDataDisk -Name "DEV-CRM-Data03" -VM $vmConfig -VhdUri $DataDiskUri -LUN 1 -Caching None -CreateOption Attach -DiskSizeInGB 1023
Update-AzureRmVM -ResourceGroupName $rgname -VM $vmConfig
<code>




 