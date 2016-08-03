---
layout: post
published: true
mathjax: false
featured: false
comments: true
title: SSRS Date Formulas Cheatsheet
tags: 'SSRS, SQL, Reporting, Dashboards'
categories:
  - SSRS
description: 'Date Calculations to dynamically generate content '
headline: SSRS Date Formulas Cheatsheet
---
While creating reports and dashboards, you may across the need to dynamically generate content based on a given date. Here are some date calculations that I use in SSRS(SQL Server Reporting Services), to dynamically generate content.  You can pass these calculated dates as default values to a data parameter that is used query a dataset.

### To retreive the first or last day of a given month

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


### To retreive a specific date on a given month: 

For Example, to get the 10th of the previous month
=dateadd(dateinterval.month, -1, today().AddDays(-(today().Day-10)))

For Example, to get the 5th of the current month
=dateadd(dateinterval.month, 0, today().AddDays(-(today().Day-5)))

For Example, to get the 20th of the next month
=dateadd(dateinterval.month, 1, today().AddDays(-(today().Day-20)))


