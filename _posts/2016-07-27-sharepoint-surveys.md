---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Create a Custom View in a SharePoint Survey
description: ''
headline: ''
modified: ''
categories: 'SharePoint'
tags: 
- SharePoint
- Office 365
imagefeature: ''
---
Surveys in SharePoint are a good way to collect feedback from employees in your organization. You can use several different types of questions, such as multiple choice, fill-in fields, and even ratings.

There are default views in Surveys like Overview, All Responses and Graphical Summary, but the Survey list settings does not give you the option to add or modify a view.

![Image]({{ site.url }}/images/blog/sharepoint-survey-views.JPG)

If you would like to create your own custom view like in other SharePoint lists, follow these steps - 

1) Open the Survey list settings and check the URL. Find the ListID from the URL.
It should include the List ID - List=%7B6253A4F3%2DCBDE%2D4F90%2D8B57%2D49BA8EB10A9A%7D

2) Now change the URL in the browser to the following URL and append your List ID
http://SiteName/_layouts/ViewType.aspx?
List=%7BF2141E9F%2D8EA2%2D42EE%2DA965%2D52F1D7362066%7D

3)Then choose your custom view style and name it.

![Image]({{ site.url }}/images/blog/sharepoint-survey-custom-view.JPG)

This is an easy way to give your survey admin good insights into surveys using custom SharePoint Views.
