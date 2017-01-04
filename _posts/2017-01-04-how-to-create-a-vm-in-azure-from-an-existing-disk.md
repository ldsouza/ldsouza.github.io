---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: How to create a VM in Azure from an existing Disk
---
<code></code><code>PowerShell
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
</code><code></code>