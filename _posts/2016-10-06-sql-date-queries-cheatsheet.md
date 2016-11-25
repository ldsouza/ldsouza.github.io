---
layout: post
published: true
mathjax: false
featured: false
comments: true
title: SQL Date Queries Cheatsheet
tags: 'SQL'
categories:
  - SQL
description: 'Date Calculations in MS SQL'
headline: Date Calculations in MS SQL
---

Here are some date formulas that you may find useful when query SQL Server-

![Image]({{ site.url }}/images/blog/sql-date-queries-cheatsheet/1.jpg)

### Date Formulas 

Current Date without Time:  
SELECT DATEADD(day, DATEDIFF(day, 0, GETDATE()), 0)

First Date of Current Month:  
SELECT DATEADD(mm, DATEDIFF(mm, 0, GETDATE()), 0)

First Date of Previous Month:  
SELECT DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) - 1, 0)

First Date of Next Month:  
SELECT DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) + 1, 0)

Last Date of Current Month:  
SELECT DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE())+1,0))

Last Date of Previous Month:  
SELECT DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE()),0))

Last Date of Next Month:  
SELECT DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE())+2,0))
