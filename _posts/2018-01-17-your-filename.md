---
layout: post
published: false
categories:
  - personal
mathjax: false
featured: false
comments: false
title: ''
---
## A New Post

Enter text in [Markdown](http://daringfireball.net/projects/markdown/). Use the toolbar above, or click the **?** button for formatting help.

Create a Azure RM Service Principal
https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-create-service-principal-portal


$pass = ConvertTo-SecureString "k1ez4gZhx48Ifv5xxNzzykzwsOgqbTRKIBA7V4AvabQ=" -AsPlainText –Force
$cred = New-Object -TypeName pscredential –ArgumentList "d17d1afe-6ce7-427e-85ca-a02fdf01fdf8@col1050.onmicrosoft.com", $pass
Login-AzureRmAccount -Credential $cred -ServicePrincipal –TenantId 35edb7bb-df3e-4c68-9814-c50f8dd7204d

Start-AzureRmAutomationRunbook -AutomationAccountName "Automation" -Name "Start-VM-DEV-CRM" -ResourceGroupName "Development"
