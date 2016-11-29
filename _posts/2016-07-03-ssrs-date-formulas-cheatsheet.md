---
layout: post
published: true
mathjax: false
featured: false
comments: true
title: SSRS Date Formulas Cheatsheet
tags: 'SSRS SQL Reporting Dashboards'
categories:
  - SSRS
description: 'Date Calculations to dynamically generate content '
headline: SSRS Date Formulas Cheatsheet
---
You may across the need to dynamically generate content, while creating reports and dashboards using SSRS (SQL Server Reporting Services). You can pass one of these calculated dates as a default value, when you query a dataset.

![Image](http://csharpcorner.mindcrackerinc.netdna-cdn.com/UploadFile/7d3362/ssrs-parameter-validation-using-custom-code/Images/SSRS%20report.jpg)

### To retrieve the first or last day of a given month  

First day of current month:  
=dateadd("m",0,dateserial(year(Today),month(Today),1))

First day of previous month:  
=dateadd("m",-1,dateserial(year(Today),month(Today),1))

First day of next month:  
=dateadd("m",1,dateserial(year(Today),month(Today),1))

Last day of current month:  
=dateadd("m",1,dateserial(year(Today),month(Today),0))

Last day of previous month:  
=dateadd("m",0,dateserial(year(Today),month(Today),0))

Last day of next month:  
=dateadd("m",2,dateserial(year(Today),month(Today),0))


### To retrieve a specific date on a given month:  

For Example, to get the 10th of the previous month  
=dateadd(dateinterval.month, -1, today().AddDays(-(today().Day-10)))

For Example, to get the 5th of the current month  
=dateadd(dateinterval.month, 0, today().AddDays(-(today().Day-5)))

For Example, to get the 20th of the next month  
=dateadd(dateinterval.month, 1, today().AddDays(-(today().Day-20)))


