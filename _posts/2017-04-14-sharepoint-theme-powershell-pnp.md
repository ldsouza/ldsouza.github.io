---
layout: post
published: false
mathjax: false
featured: false
comments: false
title: Sharepoint theme powershell pnp
---
1) you can run the following commands to install the PowerShell cmdlets:

SharePoint Online	Install-Module SharePointPnPPowerShellOnline
SharePoint 2016	Install-Module SharePointPnPPowerShell2016
SharePoint 2013	Install-Module SharePointPnPPowerShell2013


2) Download the sharepoint color palette tool -

https://www.microsoft.com/en-us/download/details.aspx?id=38182

Create a SharePoint color theme and generate a .spolor theme file.

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/2.JPG)

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/1.JPG)

3) Download the files from the github repository
<a href="https://github.com/ldsouza/Pnp-SharePoint-Branding/tree/master/Set%20SharePoint%20Theme">Download Here</a>

4) Run the Powershell script

```javascript

.\Set-SPTheme.ps1 -TargetWebUrl "https://dev.sharepoint.com/sites/marketing" -MasterUrl "seattle.m
aster"

```