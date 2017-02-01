---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: How to restrict Office 365 Groups Creation
category: Office365
tags:
  - Office365
  - Admin
  - Powershell
---

Office 365 Groups is a collaboration service that allows groups or teams in your organization to create documents, work on project plans, send emails and schedule appointments all in one place. The process to create an Office 365 Group is straightforward and very user-friendly and does not require involvement from IT. 
This is the default behavior in Office 365, but some organizations may want to restrict which users can create groups in Office 365. I will be covering how you can disable the creation of Office 365 Groups in your tenant.

![Image]({{ site.url }}/images/blog/generic/365Groups.JPG)

There are few steps to make sure you can accomplish the tasks in this post -

###1) Install Azure AD PowerShell Module and Online Services Sign-In Assitant.

Download and install the Preview version of the Azure AD PowerShell module.
http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185

You won't be able to run the Get-MsolAllSettings cmdlet if this is not installed. The Get-MsolAllSettings cmdlet will not work with GA version, so please download the preview version. This is a little confusing since the GA version is higher than the preview one.


![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/2.JPG)

Microsoft Online Services Sign-In Assistant for IT Professionals RTW
https://www.microsoft.com/en-us/download/details.aspx?id=28177

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/1.JPG)


###2) Connect to the Office 365 service and sign into your Account

```javascript 
Connect-MsolService
```

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/3.JPG)

###3) Check the company level setting for creating Groups in your Office 365 tenant.

```javascript
Get-MsolCompanyInformation
```

Verify that UsersPermissiontoCreateGroupsEnabled setting is set to True.
![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/5.JPG)

###4) Create a Security Group in Azure AD called "AllowedtoCreateGroups" and find the Object ID of this group

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/4.JPG)

```javascript
Get-MsolGroup -SearchString "AllowedtoCreateGroups"
We can now use the ObjectID to restrict Office 365 Group Creation to this group.
![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/4.JPG)
```

###5) Select the Office 365 Group settings template by running the following command

```javascript
$Setting = Get-MsolAllSettings | Where-Object { $_.DisplayName -eq “Group.Unified” }
$SettingId = $Setting.ObjectId
$Value = $Setting.GetSettingsValue()
```

###6) Now we will disable Group creation and restrict this only the group we created earlier

```javascript
$Value[“GroupCreationAllowedGroupId”] = "d79b3d44-969b-429d-b5bd-3fa89e7ab7fd"
$Value[“EnableGroupCreation”] = “false”
Set-MsolSettings -SettingId $SettingId -SettingsValue $Value

###7)Verify the new setetings of the template

```javascript
Get-MsolAllSettings
$setting=Get-MsolSettings -SettingId 1185dbae-cc14-4d61-9ab5-59ae7f6cca6b
$setting.values

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/7.JPG)


###8) Test this with a user not part of the 'AllowedtoCreateGroups' security group and you should receive the following message

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/8.JPG)

