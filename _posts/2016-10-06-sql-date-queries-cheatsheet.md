---
layout: post
published: true
mathjax: false
featured: false
comments: true
title: SQL Date Queries Cheatsheet
tags: 'SQL Date Queries Cheatsheet'
categories:
  - SQL
description: 'Date Calculations in MS SQL'
headline: Date Calculations in MS SQL
---

Here are some SQL query date formulas -

![Image]({{ site.url }}/images/blog/sql-date-queries-cheatsheet/1.jpg)

### Date Formulas 

Current Date without Time
DATEADD(day, DATEDIFF(day, 0, GETDATE()), 0)

First Date of Current Month
DATEADD(mm, DATEDIFF(mm, 0, GETDATE()), 0)

First Date of Previous Month
DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) - 1, 0)

First Date of Next Month
SELECT DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) + 1, 0)

Last Date of Current Month
DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE())+1,0))

Last Date of Previous Month
DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE()),0))

Last Date of Next Month
DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE())+2,0))