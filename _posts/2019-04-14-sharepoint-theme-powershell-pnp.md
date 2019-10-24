---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: 'Branding SharePoint Theme using PnP PowerShell '
category: SharePoint
tags:
  - SharePoint Online
  - Office 365
  - Development
  - Powershell
  - PnP
---
In this post, I will show you how to brand SharePoint with a custom theme using PnP PowerShell. You can use this example to brand site collections or subsites and set the SharePoint composed look and the master page.

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/0.JPG)

Patterns and Practices (PnP) is an open source community effort that provides solutions and real world examples that can be easily implemented with minimal effort. Some of these examples include perform complex provisioning, management and branding towards SharePoint.


### 1) Install PnP PowerShell Commands

You can run the following commands to install the PowerShell cmdlets. 

```javascript
/*SharePoint Online*/
Install-Module SharePointPnPPowerShellOnline

/*SharePoint 2016*/
Install-Module SharePointPnPPowerShell2016

/*SharePoint 2013*/	
Install-Module SharePointPnPPowerShell2013

```

To see more instructions on installing PnP PowerShell.

<a href="https://github.com/SharePoint/PnP-PowerShell#installation">PnP Powershell Install Instructions</a>

### 2) Download and Install the SharePoint Color Palette Tool

You can use the SharePoint Color Palette tool to create a customized theme for your SharePoint site. This theme can be used in SharePoint Online, SharePoint 2016 or SharePoint 2013.

<a href="https://www.microsoft.com/en-us/download/details.aspx?id=38182">Download here</a>

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/2.JPG)

### 3) Create a SharePoint color theme

Set the colors in the SharePoint Color Palette Tool and save the file as a .spcolor file.

![Image]({{ site.url }}/images/blog/sp-pnp-branding-theme/1.JPG)

### 4) Download the script files from GitHub

The script files below can be used to set the theme of SharePoint Online, SharePoint 2016 or SharePoint 2013 site. You can change the background image and the custom .spcolor file to your custom theme.

<a href="https://github.com/ldsouza/Pnp-SharePoint-Branding/tree/master/Set%20SharePoint%20Theme">Download Here</a>

### 5) Run the PowerShell Script

Set the Target Web Url to your site or subsite and set the MasterUrl to seattle.master or oslo.master.

```javascript

.\Set-SPTheme.ps1 -TargetWebUrl "https://dev.sharepoint.com/sites/marketing" -MasterUrl "seattle.m
aster"

```
After running the script, your SharePoint site should now be branded. From this example you can see the potential of PnP PowerShell and how quickly you can brand and provision sites in SharePoint.

This example was provided by Eric Overfield and you can find more excellent examples of using PnP at his GitHub Repository <a href="https://github.com/eoverfield/SP-Branding-Options">here</a>.
