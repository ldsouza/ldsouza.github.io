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

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/1.JPG)

2) Create a classic Virtual Network

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/2.JPG)

3) Enable Azure AD Domain Services in the Classic Portal

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/3.JPG)

4) Set the DNS server of the Virtual network

![Image]({{ site.url }}/images/blog/setup-aad-domain-services/3.JPG)

5) Enable synchronization of credential hashes to AAD

Run the following Powershell script replacing the relevant connector names below. To find the connector names, open Synchronization Services on the AD Connect Server and click the connectors tab.

AD CONNECTOR NAME is the connector of Type 'Active Directory Domain Services'
AAD Connector Name is the connector of Type 'Windows Azure Active Directory (Microsoft)

$adConnector = “<CASE SENSITIVE AD CONNECTOR NAME>”
$aadConnector = “<CASE SENSITIVE AAD CONNECTOR NAME>”
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter “Microsoft.Synchronize.ForceFullPasswordSync”, String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true



Challenges - 
