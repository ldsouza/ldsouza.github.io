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
