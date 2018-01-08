---
layout: post
published: true
categories:
  - personal
mathjax: false
featured: false
comments: false
title: Using Microsoft Flow with Office 365 Groups
tags: 'Office 365,SharePoint,One Drive'
category: Office 365
---

Office 365 Groups is a collaboration service that allows groups or teams in your organization to create documents, work on project plans, send emails and schedule appointments all in one place.

It comes with a SharePoint site collection where the group files are stored. Documents can be uploaded and stored in the Group documents which is the same as 'Shared Documents' Library in the SharePoint Site.

I was curious to see if I could create workflows on this default SharePoint library, so I connected to the site collection using SharePoint Designer and I was able to create workflows.

One of the goals of this whole process was to email an attachment of files uploaded in SharePoint to members of the group. This option/feature is not available out-of-the-box, so I used Microsoft flow to accomplish this.

Head over to https://flow.microsoft.com and sign in with your Office 365 account.

![Image]({{ site.url }}/images/blog/flow-365-groups/1.JPG)

Click the 'Create from Blank' button.Search for the SharePoint trigger 'When a file is created in a folder'.

Enter the Office 365 group site url in site address and select 'Shared Documents' under Folder Id. This is the default SharePoint library used by the Office 365 group.

![Image]({{ site.url }}/images/blog/flow-365-groups/2.JPG)

The next step is to select an action. Click Next Step and then add an Action. Select the 'Send an Email' action.

Enter the email address of the Office 365 group in the To field. Select the filename from the earlier SharePoint condition. In the body, enter the following for a link to the document.

replace(concat('https://contoso.sharepoint.com/sites/ogroup',triggerOutputs()['headers']['x-ms-file-path']),'','%20')

Replace your Office 365 site url in the above expression.

![Image]({{ site.url }}/images/blog/flow-365-groups/3.JPG)


![Image]({{ site.url }}/images/blog/flow-365-groups/4.JPG)


### Summary

Here is a simple example of you how you can leverage two powerful tools Microsoft Flow and Office 365 groups to get notified of a document upload in your Office 365 group site collection.
