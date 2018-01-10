---
layout: post
published: true
categories:
  - personal
mathjax: false
featured: false
comments: false
title: Getting Started with Azure Logic Apps
category: Azure
tags:
  - Azure
  - Logic Apps
  - Automation
---
In a previous post, I showed an example of you can use Micrsoft Flow to perform business process automation. Flow is a user-friendly workflow tool targeted towards business users. Azure Logic apps is a developer focused tool that allows developers to build integration solutions and define complex workflows. 

![Image]({{ site.url }}/images/blog/azure-logic-apps/1.JPG)

Using Logic Apps, you can connect and integrate data from the cloud to on-premises. It's large ecosystem of out-of-the-box cloud connectors make integration less challenging and reduces the time to develop complex solutions.

Logic Apps is a  Platform as a Service (PaAS) available in Azure, so to get started with Logic Apps, you would have to first login to an Azure subscription. After signing into Azure, search for 'Logic App' in the Azure Marketplace.

![Image]({{ site.url }}/images/blog/azure-logic-apps/2.JPG)

Enter a name for your Logic App, Select a resource group and location and you should have your first logic app ready to build.

![Image]({{ site.url }}/images/blog/azure-logic-apps/3.JPG)

We are then presented with the Logic Apps designer designed where you can create an blank app or use a popular pre-existing template for your app. The templates are good examples to use, to learn about integrating with different cloud connectors.

In this example, I will click create a Blank Logic App. The first step is to select a Trigger. The Interval duration can be defined to set how frequently you want to check if a condition has been triggered.

![Image]({{ site.url }}/images/blog/azure-logic-apps/4.JPG)

The next step is to select an Action to run after a trigger condition has been met. In this example, you see a bunch of SQL server actions which make this a useful action to integrate your on-premises databases.

![Image]({{ site.url }}/images/blog/azure-logic-apps/5.JPG)


![Image]({{ site.url }}/images/blog/azure-logic-apps/6.JPG)

![Image]({{ site.url }}/images/blog/azure-logic-apps/7.JPG)

I will be highlighting the major updates Microsoft announced at its Ignite Conference in Orlando, Florida. These exciting features connect the workplace with intelligent content management and intranets.

