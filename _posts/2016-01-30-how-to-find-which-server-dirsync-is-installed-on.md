---
layout: post
modified: 2014-07-19
category: Office 365
comments: false
mathjax: 
tags:
  - Office 365
title: How to find which server DirSync is installed on?
---

You may come across environments where you have to troubleshoot issues with DirSync, but you have no idea what the DirSync Server is. Here is a quick way to find out the DirSync server

Search Active Directory for 'MSOL' and check the description of the user account. The name of the DirSync Server should be specified in the Description.

![Image]({{ site.url }}/images/blog/Dirsync-msol.JPG)

Here is an example of the description- 

>Account created by Microsoft Azure Active Directory Connect with installation identifier '5df8955cc2f945e6ac416ae4da2e0558' running on computer 'DIRSYNC-SERVER-NAME' configured to synchronize to tenant abc.onmicrosoft.com. This account must have directory replication permissions in the local Active Directory and write permission on certain attributes to enable Hybrid Deployment.
