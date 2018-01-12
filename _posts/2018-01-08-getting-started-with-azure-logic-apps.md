---
layout: post
published: true
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
In a previous post, I showed an example of you can use Microsoft Flow to automate your business processes. Flow is a user-friendly workflow tool targeted towards business users. Azure Logic apps is a developer focused tool that allows developers to build integration solutions and define complex workflows. 

![Image]({{ site.url }}/images/blog/azure-logic-apps/1.JPG)

Using Logic Apps, you can connect and integrate data from the cloud to on-premises. It's large ecosystem of out-of-the-box cloud connectors makes integration less challenging and reduces the time to develop complex solutions.

Logic Apps is a  Platform as a Service (PaAS) available in Azure, so to get started with Logic Apps, you would have to first login into an Azure subscription. After signing into Azure, search for 'Logic App' in the Azure Marketplace.

![Image]({{ site.url }}/images/blog/azure-logic-apps/2.JPG)

Enter a name for your Logic App, Select a resource group and location and you should have your first logic app ready to build.

![Image]({{ site.url }}/images/blog/azure-logic-apps/3.JPG)

We are then presented with the Logic Apps designer, where you can create an blank app or use popular pre-existing templates for your app. The templates are good examples to quickly get started and learn about integrating with different cloud connectors.

In this example, I will click create a Blank Logic App. 

![Image]({{ site.url }}/images/blog/azure-logic-apps/4.JPG)

The first step is to select a Trigger. The Interval duration can be defined to set how frequently you want to check if a condition has been triggered.

![Image]({{ site.url }}/images/blog/azure-logic-apps/5.JPG)

The next step is to select an Action to run after a trigger condition has been met. In this example, you see a bunch of SQL server actions which make this a useful action to integrate your on-premises databases in your app.

![Image]({{ site.url }}/images/blog/azure-logic-apps/6.JPG)

Before deploying your app, make sure to use the pricing calculator to determine how much Azure Logic Apps will cost you. The good thing is that it is consumption based, so you only pay for usage. 

But it is important to be mindful how frequently you set the polling interval in your trigger, because that can easily increase how much you pay.

Here is an excellent article explaining the pricing model -  [Logic Apps Pricing Explained](https://peter.intheazuresky.com/2017/02/24/be-careful-of-the-logic-app-consumption-prizing-model/)

![Image]({{ site.url }}/images/blog/azure-logic-apps/7.JPG)

In future posts, I will explain in detail the differences between Microsoft Flow and Azure Logic Apps and when does it make sense to use one versus the other.

