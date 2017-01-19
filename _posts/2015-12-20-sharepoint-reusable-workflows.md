---
layout: post
title: How to create Reusable Workflows in SharePoint
excerpt: >-
  How to create Reusable Workflows in SharePoint
modified: {}
categories: SharePoint
tags:
  - SharePoint Online
  - Office 365
comments: false
share: true
published: true
---

Have you created a workflow and then had to create a separate workflow for another list or library that had a similar workflow requirement? This is where you can leverage reusable workflows to make the process less time consuming and easier to manage. A reusable workflow is not created for a specific list or library but instead is created on a content type and then associated to multiple lists or libraries. 

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/1.JPG)

In this example, three different teams would like to track their daily activity in individual lists independent of each other. I would like to create a single reusable workflow to update the title of the daily activity in each of the three lists without creating three separated workflows.

#### Create Custom Lists 

The first step is to create three custom lists Whiteboard ACT1, Whiteboard ACT2, Whiteboard ACT3 to store the respective team's daily activities. We will then create site columns for the metadata, that is common across each of the three lists.

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/2.JPG)

#### Create a Custom Content Type 

The next step is to create a site content type 'Whiteboard' and add the site columns to the site content type. Then add the site content type to each of the custom lists.

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/3.JPG)

#### Create a Reusable Workflow 

Open the site in SharePoint Designer and select "Reusable Workflow".  

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/4.JPG)

Enter the name of the workflow and the content type to associate with the workflow. We will select the content type we just created. 

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/5.JPG)

Create the workflow logic just like a regular workflow and save and publish the workflow. In this example, my workflow will update the title depending on the Contact Type field.

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/6.JPG)

#### Associate the Reusable Workflow to a List 

From the top ribbon, select "Associate to List". Select the list you want this workflow to be associated with.

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/7.JPG)

Provide a name for the workflow and workflow settings like start options. Repeat the same step for the other 2 lists and then test your workflow.

![Image]({{ site.url }}/images/blog/sharepoint-reusable-workflows/8.JPG)

Any time you have to make a change to the reusable workflow, you update it once and it should apply to all the associated lists. I hope this quick demo demonstrated the power of reusable workflows and how you can implement it in your solutions.




