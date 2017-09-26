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

Here are some SQL queries that I find very useful when writing stored procedures. Using these queries, you can easily find the first date and last date of the current month, previous month or next month. 

![Image]({{ site.url }}/images/blog/sql-date-queries-cheatsheet/1.jpg)

#### Current Date without Time:  
SELECT DATEADD(day, DATEDIFF(day, 0, GETDATE()), 0)

#### First Date of Current Month:  
SELECT DATEADD(mm, DATEDIFF(mm, 0, GETDATE()), 0)

#### First Date of Previous Month:  
SELECT DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) - 1, 0)

#### First Date of Next Month:  
SELECT DATEADD(mm, DATEDIFF(mm, 0, GETDATE()) + 1, 0)

#### Last Date of Current Month:  
SELECT DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE())+1,0))

#### Last Date of Previous Month:  
SELECT DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE()),0))

#### Last Date of Next Month:  
SELECT DATEADD(s,-1,DATEADD(mm, DATEDIFF(m,0,GETDATE())+2,0))

#### Convert Date to YYYYMMDD
SELECT CONVERT(VARCHAR(10), Now(), 112)
