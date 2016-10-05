---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: SSIS - Remove Duplicate Rows
category: SQL Server
tags:
- SQL Server
- SSIS
---
There are several ways to remove duplicate records during an ETL process. An easy way to accomplish this is using the SSIS Sort Transformation.

Create a Data Flow Task in SSIS. Drag an OLEDB Source task, Sort Transformation and OLEDB Destination task to the Design screen.

![Image]({{ site.url }}/images/blog/SSIS-remove-duplicates.JPG)

Configure the Sort Transformation and select the field that your want to sort by and remove duplicates. Select the checkbox to 'Remove rows with duplicate sort values'.

![Image]({{ site.url }}/images/blog/SSIS-remove-duplicates1.JPG)

