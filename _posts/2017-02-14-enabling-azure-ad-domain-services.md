---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: Enabling Azure AD Domain Services
---
##Azure Active Directory (AAD) Domain Services is a Domain Service that allows you to use on-premises AD credentials to connect to your resources in Azure without installing and maintaining additional identity infrastructure in the cloud. 

Some of the features AAD Domain Services provides are Domain join, Domain Authentication using  NTLM/Kerberos Authentication and Group Policy.

To setup AAD Domain Services -

1) Create a Group called 'AAD DC Administrators'

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/2.JPG)

2) Create a classic Virtual Network

3) Enable Azure AD Domain Services in the Classic Portal

4) Enable synchronization of credential hashes to AAD

Challenges - 
