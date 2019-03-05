---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: How to restrict the creation of Office 365 Groups
category: Office 365
tags:
  - Office 365
  - Admin
  - Powershell
---

Office 365 Groups is a collaboration service that allows groups or teams in your organization to create documents, work on project plans, send emails and schedule appointments all in one place.

![Image]({{ site.url }}/images/blog/generic/365Groups.JPG)

The process to create an Office 365 Group is straightforward and very user-friendly and does not require involvement from IT. 
Some organizations may want to have a governance plan in place first and may want to restrict which users can create groups in Office 365. Below are the steps you can take to disable the creation of Office 365 Groups in your tenant.


### Install the Azure AD PowerShell Module and the Online Services Sign-In Assistant.

Download and install the Preview version of the Azure AD PowerShell module.

[Download Azure AD PowerShell module](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185 "Download Azure AD PowerShell module")

You will not be able to run the Get-MsolAllSettings cmdlet if this is not installed. The Get-MsolAllSettings cmdlet will only work with the preview version and not the GA version. This is a little confusing since the GA version is higher than the preview one.

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/2.JPG)

Download and install the Online Services Sign-In Assistant.

[Download Microsoft Online Services Sign-In Assistant](https://www.microsoft.com/en-us/download/details.aspx?id=28177 "Microsoft Online Services Sign-In Assistant")

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/1.JPG)



#### Connect to the Office 365 service and sign into your Account.

```javascript 
Connect-MsolService
```

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/3.JPG)


#### Check the company level setting for creating Groups in your Office 365 tenant.

```javascript
Get-MsolCompanyInformation
```

Verify that <b>UsersPermissiontoCreateGroupsEnabled<b> setting is set to True.

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/5.JPG)


#### Create a Security Group in Azure AD called "AllowedtoCreateGroups" and find the Object ID of this group.


![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/4.JPG)

```javascript
Get-MsolGroup -SearchString "AllowedtoCreateGroups"
```

We can now use the ObjectID to restrict Office 365 Group Creation to this group.

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/4.JPG)


#### Select the Office 365 Group settings template by running the following cmdlet.

```javascript
$Setting = Get-MsolAllSettings | Where-Object { $_.DisplayName -eq “Group.Unified” }
$SettingId = $Setting.ObjectId
$Value = $Setting.GetSettingsValue()
```


#### Disable Group creation and restrict creation to only the group we created earlier.

```javascript
$Value[“GroupCreationAllowedGroupId”] = "d79b3d44-969b-429d-b5bd-3fa89e7ab7fd"
$Value[“EnableGroupCreation”] = “false”
Set-MsolSettings -SettingId $SettingId -SettingsValue $Value
```


#### Verify the new settings of the template.

```javascript
Get-MsolAllSettings
$setting=Get-MsolSettings -SettingId 1185dbae-cc14-4d61-9ab5-59ae7f6cca6b
$setting.values
```

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/7.JPG)



#### Test this with a user not part of the 'AllowedtoCreateGroups' security group

You should receive the following message.

![Image]({{ site.url }}/images/blog/restrict-365-groups-creation/8.JPG)


#### If the above steps do not work, try the following steps instead. Get the Group Name

```javascript
$GroupName = "AllowedtoCreateO365Groups"
$AllowGroupCreation = "False"
```

#### Run the following script to restrict the creating of Groups

```javascript
Connect-AzureAD

$settingsObjectID = (Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ).id
if(!$settingsObjectID)
{
	  $template = Get-AzureADDirectorySettingTemplate | Where-object {$_.displayname -eq "group.unified"}
    $settingsCopy = $template.CreateDirectorySetting()
    New-AzureADDirectorySetting -DirectorySetting $settingsCopy
    $settingsObjectID = (Get-AzureADDirectorySetting | Where-object -Property Displayname -Value "Group.Unified" -EQ).id
}

$settingsCopy = Get-AzureADDirectorySetting -Id $settingsObjectID
$settingsCopy["EnableGroupCreation"] = $AllowGroupCreation

if($GroupName)
{
	$settingsCopy["GroupCreationAllowedGroupId"] = (Get-AzureADGroup -SearchString $GroupName).objectid
}

Set-AzureADDirectorySetting -Id $settingsObjectID -DirectorySetting $settingsCopy

(Get-AzureADDirectorySetting -Id $settingsObjectID).Values
```
