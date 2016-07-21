---
layout: post
title: SharePoint Reusable Workflows
excerpt: >-
  How to modify the column order in a libary or list form
modified: {}
categories: SharePoint
tags:
  - SharePoint Online
  - Office 365
comments: true
share: true
published: true
---

Here is a helpful tip that I often use, whenever I have to add custom columns to a list or library. SharePoint, by default, arranges the column order in the order that you add custom columns to a list or library. There are often times when you may have to modify this order.

Create three custom lists Whiteboard ACT1, Whiteboard ACT2, Whiteboard ACT3. You may come across situations like this where you have mutiple lists that have to be separated but they share common set of reuirements.

In this case, three different teams would track their daily work in individual lists and this is the reason for separating them. I created site columns for the metadata that is common across each list.

Create a site content type 'Whiteboard' and add the site columns to the site content type. Now add the site content type to each of the custom lists.

I would now to like to apply a 

In this example, I would like 'Client' to come before 'Stage'. This applies to the New, Edit and Display Forms.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/sharepoint-tip-column-order-before.JPG" alt="image">
</figure>


