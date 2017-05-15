---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: Powershell List
---
## A New Post

Powershell ISE
. $pshome\powershell_ise

PS C:\Windows\system32> Get-Command -Module azurerm

PS C:\Windows\system32> get-module -ListAvailable | where name -Like "*Azure*"

PS C:\Windows\system32> get-module -ListAvailable | where name -Like "*Azure*" |foreach {get-command -Module $_}

PS C:\Windows\system32> Get-Command -verb new

## Install Azure Module
install-module Azurerm
Update-module AzureRM
import-module AzureRM
(get-module AzureRM).Version

## Logging into Azure
Login-AzureRMAccount
Azure service manager - Add-AzureAccount

$cred = get-credential
 Login-AzureRMAccount -Credential $cred


**Save a Password Securely to Use with PowerShell**
http://windowsitpro.com/development/save-password-securely-use-powershell

**Azure Subscription**
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionId 'a984cf58-3128-46e3-baa2-f5e5d915b560'
Get-AzureRmStorageAccount | ft StorageAccountName, ResourceGroupName
Get-AzureRmContext


http://savilltech.com/blog/automating-deployments-to-azure-iaas-with-custom-actions/


