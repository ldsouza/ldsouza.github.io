---
layout: post
title: Implementing a Business Development/Sales Pipeline in SharePoint (Part 3)
description: >-
  Part 3 of a Quick and Easy Solution to track your Sales Opportunities in
  SharePoint.
modified: 'Tue Jul 05 2016 20:00:00 GMT-0400 (Eastern Daylight Time)'
category: SharePoint
tags:
  - SharePoint Online
  - Office 365
  - SharePoint
comments: true
mathjax: false
published: true
featured: false
---

This is a blog post in the series “Implementing a Business Development/Sales Pipeline in SharePoint”.  In this series, I will show you how to implement a Pipeline to manage and track your Sales or Development Opportunities.

In <a href="{{ site.github.url }}/sharepoint/sharepoint-sales-pipeline">Part 1</a> of this series, we have already setup a Custom list named Pipeline to track Opportunities and their status. We added the metadata columns associated to an opportunity and modified the default view. 

In <a href="{{ site.github.url }}/sharepoint/sharepoint-sales-pipeline-2">Part 2</a> of this series, we added custom views to easily group and view information in the Pipeline.


In this blog post, we will look at a scenario where it is possible for an Opportunity to be in multiple stages simultaneously. Because of this, we are unable to group by 'Stage' to have a count of the Opportunities by Stage.

## Change the 'Stage' Column to Allow Multiple Selections

In List Settings, click the column Stage and change the setting to Checkboxes.

![Image]({{ site.url }}/images/blog/pipeline3-column-multiple.JPG)

---

## Create Additional Columns to Track each Stage

In this example, I created 'Single line of Text' columns for each of the Stages like (Prospecting, Won, Lost).

![Image]({{ site.url }}/images/blog/pipeline3-column-stages.JPG)

Modify the View to Count each of the new Columns.

![Image]({{ site.url }}/images/blog/pipeline3-view-count.JPG)

After modifying the view, you should see a view with Count=0 for all the stages.

![Image]({{ site.url }}/images/blog/pipeline3-view-count1.JPG)

---

## Create a Workflow to count the number of Opportunities in each stage

We will create a workflow to check the status set by the user and update the corresponding new stage columns we just created. We want this workflow to run any time an opportunity is added or modified.
Connect to your Site using SharePoint Designer, Open the Pipeline List in Lists and Libraries and Create a New SharePoint 2013 Workflow.

![Image]({{ site.url }}/images/blog/pipeline3-new-workflow.JPG)

Select Actions from the Ribbon and select 'Set Workflow Variable'. Create a new variable named 'Stage' and set it to the Current Item 'Stage'.

![Image]({{ site.url }}/images/blog/pipeline3-workflow1.JPG)

Select 'If any value equals value' condition and set the condition to the check if the variable 'Stage' contains 'Won'. If it matches this condition, Update 'Won' to 1 else if it does not contain Won then leave it blank.

Create If Conditions for each one of the Stages and Save and Publish the Workflow.

![Image]({{ site.url }}/images/blog/pipeline3-workflow2.JPG)

Also, change the worfklow Start Options to run when an item is created and when it is changed. This will count the opportunities from the time they are added into the Pipeline.

![Image]({{ site.url }}/images/blog/pipeline3-workflow-options.JPG)


We can now see a Count of Opportunities in each of the Stages in our view.

![Image]({{ site.url }}/images/blog/pipeline3-final-view.JPG)
