---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Connecting to Azure using a Non-Interactive Login
tags: 'Azure,Automation'
category: Azure
categories:
  - personal
---
In this post, I will login to Azure non-interactively using an Azure Active Directory Application and an Azure Resource Manager Service Principal. This is very useful when you want to automate your Azure scripts and run them on a schedule or without requiring an interactive login.

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/0.JPG)

### 1) Create an Azure Active Directory application

Login to your Azure Subscription using the Portal and click on Azure Active Directory and select App Registrations.

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/1.JPG)

Click 'New Application Registration' to register our application with Azure Active Directory. 

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/2.JPG)

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/3.JPG)

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/4.JPG)

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/5.JPG)

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/6.JPG)

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/7.JPG)

### 2) Create an Azure RM Service Principal

https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal



### 2) Create the Tenant ID




$pass = ConvertTo-SecureString "k1ez4gZhx48Ifv5xxNzzykzwsOgqbTRKIBA7V4AvabQ=" -AsPlainText –Force
$cred = New-Object -TypeName pscredential –ArgumentList "d17d1afe-6ce7-427e-85ca-a02fdf01fdf8@col1050.onmicrosoft.com", $pass
Login-AzureRmAccount -Credential $cred -ServicePrincipal –TenantId 35edb7bb-df3e-4c68-9814-c50f8dd7204d

Start-AzureRmAutomationRunbook -AutomationAccountName "Automation" -Name "Start-VM-DEV-CRM" -ResourceGroupName "Development"


https://kasperk.it/microsoft/login-azurermaccount-command-found-module-azurerm-profile-module-not-loaded
