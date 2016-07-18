---
layout: post
title: "SharePoint Tip - Change the column order in a form"
description: How to modify the column order in a libary or list form
headline: 
modified: 2014-07-19
category: SharePoint
tags: [SharePoint, Office 365]
comments: true
mathjax: 
---

Here is a helpful tip that I often use, whenever I have to add custom columns to a list or library. SharePoint, by default, arranges the column order in the order that you add custom columns to a list or library. There are often times when you may have to modify this order.

In this example, I would like 'Client' to come before 'Stage'. This applies to the New, Edit and Display Forms.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-column-order-before.JPG" alt="image">
</figure>


Navigate to your SharePoint List or Library. Click on the Tab named 'List' or 'Library' and select 'List Settings' or 'Library Settings'.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-list-settings1.JPG" alt="image">
</figure> 
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-list-settings2.JPG" alt="image">
</figure> 

Click on Advanced Settings under General Settings. Select Yes for 'Allow management of Content Types' and click Ok to save this setting.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-advanced-settings.JPG" alt="image">
</figure>

Now a new section appears in the List or Library settings. 'Item' is the default content type of a list and 'Document' is the default content type of a Document Library. Click on 'Item' or 'Document' and then select Column Order.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-advanced-contenttype.JPG" alt="image">
</figure>

Re-arrange the column order according to your requirments and now the new or edit form of your list/library will reflect the changes.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-advanced-column-order.JPG" alt="image">
</figure>

After changing the column order in the content type, I can see my desired result.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-column-order-after.JPG" alt="image">
</figure>