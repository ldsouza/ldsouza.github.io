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

install-module Azurerm
Update-module AzureRM
import-module AzureRM
(get-module AzureRM).Version

Login-AzureRMAccount

Azure service manager - Add-AzureAccount



