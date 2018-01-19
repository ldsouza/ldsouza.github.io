---
layout: post
published: false
categories:
  - personal
mathjax: false
featured: false
comments: false
title: Automating  your Connection to Azure
---
In this post, I will show you how to login to Azure non-interactively using an Azure Active Directory Application and an Azure Resource Manager Service Principal. This is very useful when you want to automate your Azure scripts and run them on a schedule or without requiring an interactive login.

### 1) Create an Azure Active Directory application



### 2) Create an Azure RM Service Principal

https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal

### 2) Create the Tenant ID


$pass = ConvertTo-SecureString "k1ez4gZhx48Ifv5xxNzzykzwsOgqbTRKIBA7V4AvabQ=" -AsPlainText –Force
$cred = New-Object -TypeName pscredential –ArgumentList "d17d1afe-6ce7-427e-85ca-a02fdf01fdf8@col1050.onmicrosoft.com", $pass
Login-AzureRmAccount -Credential $cred -ServicePrincipal –TenantId 35edb7bb-df3e-4c68-9814-c50f8dd7204d

Start-AzureRmAutomationRunbook -AutomationAccountName "Automation" -Name "Start-VM-DEV-CRM" -ResourceGroupName "Development"
