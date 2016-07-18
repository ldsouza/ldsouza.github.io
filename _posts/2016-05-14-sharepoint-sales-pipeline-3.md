---
layout: post
title: Implementing a Business Development/Sales Pipeline in SharePoint (Part 3)
excerpt: >-
  Part 3 of a Quick and Easy Solution to track your Sales Opportunities in SharePoint.
modified: {}
categories: blog
tags:
  - SharePoint
  - Office 365
comments: true
share: true
published: true
---

This is a blog post in the series “Implementing a Business Development/Sales Pipeline in SharePoint.”  In this series, I’ll show you how to implement a Pipline to manage and track opportunities.

In <a href="{{ site.github.url }}/blog/sharepoint-sales-pipeline/">Part 1</a> of this series, we have already setup a Custom list named Pipeline to track Opportunities and their status. We added the metadata columns associated to an opportunity and modified the default view. 

In <a href="{{ site.github.url }}/blog/sharepoint-sales-pipeline-2/">Part 2</a> of this series, we added custom views to easily group and view information in the Pipeline.


In this part, we will look at a scenario where it is possible for an Opportunity to be in multiple stages simultaneously. Because of this, we are unable to group by 'Stage' to have a count of the Opportunities by Stage.

## Change the 'Stage' Column to Allow Multiple Selections

In List Settings, click the column Stage and change the setting to Checkboxes.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-column-multiple.JPG" alt="image">
</figure> 

## Create Additional Columns to Track each Stage

In this example, I created 'Single line of Text' columns for each of the Stages like (Prospecting, Won, Lost)
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-column-stages.JPG" alt="image">
</figure> 

Modify the View to Count each of the new Columns.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-view-count.JPG" alt="image">
</figure> 

After modifying the view, you should see a view with Count=0 for all the stages.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-view-count1.JPG" alt="image">
</figure> 

## Create a Workflow to count the number of Opportunities in each stage

We will not create a workflow to check the status selected or deselected by the user and update the corresponding new stage columns we just created. We want this workflow to run any time an opportunity is added or modified.
Connect to your Site using SharePoint Designer, Open the Pipeline List in Lists and Libraries and Create a New SharePoint 2013 Workflow
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-new-workflow.JPG" alt="image">
</figure> 

Select Actions from the Ribbon and select 'Set Workflow Variable'. Create a new variable named 'Stage' and set it to the Current Item 'Stage'.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-workflow1.JPG" alt="image">
</figure> 

Select 'If any value equals value' condition and set the condition to the check if the variable 'Stage' contains 'Won'. If it matches this condition, Update 'Won' to 1 else if it does not contain Won then leave it blank.

Create If Conditions for each one of the Stages and Save and Publish the Workflow.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-workflow2.JPG" alt="image">
</figure> 

Also, change the worfklow Start Options to run when an item is created and when it is changed. This will count the opportunities from the time they are added into the Pipeline.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-workflow-options.JPG" alt="image">
</figure> 


We can now see a Count of Opportunities in each of the Stages in our view.
<figure>
<img src="https://raw.githubusercontent.com/ldsouza/ldsouza.github.io/master/images/blog/pipeline3-final-view.JPG" alt="image">
</figure> 
