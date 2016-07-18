---
layout: post
title: "Implementing a Business Development/Sales Pipeline in SharePoint (Part 1)"
description: Part 1 of a Quick and Easy Solution to track your Sales Opportunities in SharePoint.
headline: 
modified: 2016-07-06
category: SharePoint
tags: [SharePoint, Office 365]
comments: true
mathjax: 
---

This is a blog post in the series “Implementing a Business Development/Sales Pipeline in SharePoint.”  In this series, I’ll show you how to implement a Pipline to manage and track opportunities.
If you don't have a CRM or an Opportunity tracking system, here is a quick and easy way to build a robust and efficient solution.

The Basic Requirements

- Track Opportunities and their status
- Ability to look at historical and current Opportunities
- Track the sales person/owner of the opportunity

## Create a Custom List in SharePoint

The first thing to do is to create a custom list and add the necessary metadata you would like to associate with an Opportunity.
![Image]({{ site.url }}/images/blog/pipeline-custom-list.JPG)

Add the opportunity metadata colmns like Stage(Choice), Projected Revenue(Currency), Opportunity Owner(Person or Group). You can add more metadata like Lead Source, Rating depending on your business requirements.
![Image]({{ site.url }}/images/blog/pipeline-metadata.JPG)

Before we begin adding new opportunities, rename the default sharepoint list column 'Title' to 'Opportunity Name'.
![Image]({{ site.url }}/images/blog/pipeline-rename-title.JPG)

## Add New Opportunities

Select New Item to begin adding Opportunities to your Pipeline.
![Image]({{ site.url }}/images/blog/pipeline-new-edit.JPG)
![Image]({{ site.url }}/images/blog/pipeline-new-item.JPG) 


> SharePoint Tip - <a target="_blank" href ="/blog/sharepoint-tip-column-order/">Learn how to change the column order in a form</a>


If you have existing opportunities in Excel, you can easily bulk update them in SharePoint.
![Image]({{ site.url }}/images/blog/pipeline-excel-upload.JPG)

Select 'Edit', select the first cell to paste into and Press 'Control + V' on your keyboard. Select 'Stop' to save your changes.
![Image]({{ site.url }}/images/blog/pipeline-excel-upload1.JPG)

## Modify the Default View

To display a sum of the Projected Revenue in my SharePoint View, select 'Modify View' from the List tab, scroll down to the Totals Section and select 'Sum' as the Total.
![Image]({{ site.url }}/images/blog/pipeline-modify-view.JPG)

![Image]({{ site.url }}/images/blog/pipeline-default-view.JPG)

This is a quick overview on implementing a Business Development/Sales Pipeline tro track and manage your opportunities. In the next part of this blog post series, I will cover some advanced functionality that you could add to this solution.

<a href="{{ site.github.url }}/blog/sharepoint-sales-pipeline-2/">Implementing a Business Development/Sales Pipeline in SharePoint (Part 2)</a>
