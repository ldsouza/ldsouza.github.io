---
layout: post
title: Change the great order in a SharePoint Form
excerpt: "Just about everything you'll need to style in the theme: headings, paragraphs, blockquotes, tables, code blocks, and more."
modified: 2016-06-01T14:17:25-04:00
categories: articles
tags: [sample-post]
image:
  feature: so-simple-sample-image-1.jpg
  credit: WeGraphics
  creditlink: http://wegraphics.net/downloads/free-ultimate-blurred-background-pack/
comments: true
share: true
---

Here is a helpful tip that I often use, whenever I have to add custom columns to a list or library. SharePoint, by default, arranges the column order in the order that you add custom columns to a list or library. There are often times when you may have to modify this order.

In this example, I would like 'Client' to come before 'Stage'. This applies to the New, Edit and Display Forms.
![Column]({{ site.url }}/images/blog/sharepoint-tip-column-order-before.JPG)

Navigate to your SharePoint List or Library. Click on the Tab named 'List' or 'Library' and select 'List Settings' or 'Library Settings'.
![Column]({{ site.url }}/images/blog/sharepoint-tip-list-settings1.JPG)
![Column]({{ site.url }}/images/blog/sharepoint-tip-list-settings2.JPG)

Click on Advanced Settings under General Settings. Select Yes for 'Allow management of Content Types' and click Ok to save this setting.
![Column]({{ site.url }}/images/blog/sharepoint-tip-advanced-settings.JPG)

Now a new section appears in the List or Library settings. 'Item' is the default content type of a list and 'Document' is the default content type of a Document Library. Click on 'Item' or 'Document' and then select Column Order.
![Column]({{ site.url }}/images/blog/sharepoint-tip-advanced-contenttype.JPG)

Re-arrange the column order according to your requirments and now the new or edit form of your list/library will reflect the changes.
![Column]({{ site.url }}/images/blog/sharepoint-tip-advanced-column-order.JPG)

After changing the column order in the content type, I can see my desired result.
![Column]({{ site.url }}/images/blog/sharepoint-tip-column-order-after.JPG)