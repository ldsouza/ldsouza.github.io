---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Connecting to Azure using a Non-Interactive Login
tags:
  - Azure
  - Automation
  - Powershell
category: Azure
---
In this post, I will login to Azure non-interactively using an Azure Active Directory Application and an Azure Resource Manager Service Principal. This is very useful when you want to automate your Azure scripts and run them on a schedule or without requiring an interactive login.

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/0.JPG)

### 1) Create an Azure Active Directory application

Login to your Azure Subscription using the Portal and click on Azure Active Directory and select App Registrations.

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/1.JPG)

Click 'New Application Registration' to register our application with Azure Active Directory. 

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/2.JPG)

Enter and name and url for your Application. Select Web app / API for the type of application and then click Create.

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/3.JPG)

### 2) Get the Application ID and Authentication key

After creating the Application, we now need to get the Application ID and Key, so we can login non-interactively. Copy the Application ID of your application.

To generate an authentication key, select keys and enter a description for the key and its expiration. Copy the key displayed.

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/4.JPG)

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/5.JPG)


https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal



### 3) Get the Tenant ID or Directory ID

Select Azure Active Directory again, and now select Properties for your Azure AD. Copy the Directory ID. This value is the same as your tenant ID.

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/6.JPG)

![Image]({{ site.url }}/images/blog/azure-login-non-interactive/7.JPG)


### 4) Login to Azure Programmatically

First we will convert our authentication key from to a secure strings 

```javascript
$pass = ConvertTo-SecureString "<Authentication Key>" -AsPlainText –Force
```
  
Your Application ID is appended to your tenant URL @xxx.onmicrosoft.com


```javascript 
$cred = New-Object -TypeName pscredential –ArgumentList "<Application ID>@xxx.onmicrosoft.com", $pass
  
Login-AzureRmAccount -Credential $cred -ServicePrincipal –TenantId <Tenant ID>
```


### Issues

The ‘Login-AzureRmAccount’ command was found in the module ‘AzureRM.Profile’, but the module could not be loaded

If you get the following error message, you can fix this using the following powershell command with elevated permissions. 

```javascript
Set-ExecutionPolicy RemoteSigned
```
