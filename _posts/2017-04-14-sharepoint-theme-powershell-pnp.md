---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: 'Branding SharePoint Theme using PnP PowerShell '
category: SharePoint
tags: 'SharePoint Online,Development,SharePoint'
---
In this post, I will show you how to brand SharePoint with a custom theme using PnP PowerShell. You can use this example to brand site collections or subsites, set the SharePoint composed look and the master page.

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/0.JPG)

Patterns and Practices (PnP) is an open source community effort that provides solutions and real world examples that can be easily implemented with minimal effort.Some of these examples include perform complex provisioning, management and branding towards SharePoint.


### 1) Install PnP Powershell

you can run the following commands to install the PowerShell cmdlets:

```javascript
/*SharePoint Online*/
Install-Module SharePointPnPPowerShellOnline

/*SharePoint 2016*/
Install-Module SharePointPnPPowerShell2016

/*SharePoint 2013*/	
Install-Module SharePointPnPPowerShell2013

```

### 2) Download  and Install the sharepoint color palette tool -

https://www.microsoft.com/en-us/download/details.aspx?id=38182

### 3) Create a SharePoint color theme and generate a .spolor theme file.

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/2.JPG)

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/1.JPG)

### 4) Download the files from the github repository
<a href="https://github.com/ldsouza/Pnp-SharePoint-Branding/tree/master/Set%20SharePoint%20Theme">Download Here</a>

### 5) Run the Powershell script

```javascript

.\Set-SPTheme.ps1 -TargetWebUrl "https://dev.sharepoint.com/sites/marketing" -MasterUrl "seattle.m
aster"

```
