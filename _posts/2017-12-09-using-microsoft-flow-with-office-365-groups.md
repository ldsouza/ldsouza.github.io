---
layout: post
published: true
mathjax: false
featured: false
comments: false
category: Office 365
tags:
  - SharePoint Online
  - Office 365
  - SharePoint
  - Office 365 Groups
title: Using Microsoft Flow with Office 365 Groups
---

Office 365 Groups is a collaboration service that allows groups or teams in your organization to create documents, work on project plans, send emails and schedule appointments all in one place.

![Image]({{ site.url }}/images/blog/flow-365-groups/1.JPG)

A Office 365 group comes with a SharePoint site collection where the group files are stored. Documents can be uploaded and stored in  Group documents which is the same as the 'Shared Documents' Library in the SharePoint Site.

When a file is uploaded online, the members of the group are not notified. We can leverage Microsoft Flow to create a flow to email an attachment to members of the group, when a document is uploaded to the library.

The first step is to head over to https://flow.microsoft.com and sign in with your Office 365 account.

Click the 'Create from Blank' button. Select the SharePoint trigger 'When a file is created in a folder'.

![Image]({{ site.url }}/images/blog/flow-365-groups/2.JPG)

Enter the Office 365 group site url under site address and select 'Shared Documents' under Folder Id. This is the default SharePoint library used by the Office 365 Group.

![Image]({{ site.url }}/images/blog/flow-365-groups/3.JPG)

The next step is to select an action to send the group and email with the document attached. Click Next Step and then add an Action. Select the 'Send an Email' action.

Enter the email address of the Office 365 group in the To field. Select the filename from the earlier SharePoint condition. In the body, enter the following for a link to the document.

replace(concat('https://contoso.sharepoint.com/sites/ogroup',triggerOutputs()['headers']['x-ms-file-path']),'','%20')

Replace your Office 365 site url in the above expression.

![Image]({{ site.url }}/images/blog/flow-365-groups/4.JPG)


### Summary

Here is a simple example of you how you can leverage two powerful tools Microsoft Flow and Office 365 groups to get notified of a document upload in your Office 365 group site collection and access the document directly from your email.
