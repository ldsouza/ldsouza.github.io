---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: Supercharge your Power BI Data Model by adding a Date Table
headline: Supercharge your Power BI Data Model by adding a Date Table
tags:
- Power BI
- Data Modeling
- Reporting
categories:
  - Power BI
---

Power BI Desktop is a powerful data exploration and reporting tool that can be used to import data into the Power BI data model from several data sources. Once you have imported data from multiple sources, you can create relationships between the tables and visualize data on dashboards and reports. In this post, I will show you how to supercharge your Power BI Data Model by adding a date table and help your filter your dashboards and reports using date filters from a single source.

![Image]({{ site.url }}/images/blog/powerbi-add-a-date-table/0.JPG)

For every dataset you import into Power BI, you generally have a date timestamp like a transaction date or an order date. The benefit of using a tool like Power BI, is that it helps us take disparate data sources and allows us to visualize them on a single dashboard or report. Instead of having multiple filters and/or slicers using these different date columns, a better approach instead is to use a date table or a date dimension from a warehouse. If you do not have an existing date table in a database or a warehouse, you can add one in Power BI itself.

Here is a step-by-step guide:

### 1) Create a Date Table in Power BI Using DAX 

Select the Modeling Tab in Power BI Desktop and select New Table. Paste in the DAX code below and click Enter.

![Image]({{ site.url }}/images/blog/powerbi-add-a-date-table/1.JPG)

```javascript
DimDate =
VAR fiscal_year_end_month = 3
RETURN
    ADDCOLUMNS (
        CALENDARAUTO ( fiscal_year_end_month ),
        "DateAsInteger", FORMAT ( [Date], "YYYYMMDD" ),
        "Year", YEAR ( [Date] ),
        "Fiscal Year", IF (
            MONTH ( [DATE] ) <= fiscal_year_end_month,
            YEAR ( [DATE] ) - 1,
            YEAR ( [DATE] )
        ),
        "Quarter", "Q" & FORMAT ( [Date], "Q" ),
        "Fiscal Quarter", "Q"
            & FORMAT (
                IF (
                    fiscal_year_end_month < MONTH ( [Date] ),
                    DATE ( YEAR ( [Date] ), MONTH ( [Date] ) - fiscal_year_end_month, 1 ),
                    DATE ( YEAR ( [Date] ) - 1, MONTH ( [Date] ) + 12 - fiscal_year_end_month, 1 )
                ),
                "Q"
            ),
        "YearQuarter", FORMAT ( [Date], "YYYY" ) & "/Q"
            & FORMAT ( [Date], "Q" ),
        "Fiscal YearQuarter", IF (
            MONTH ( [DATE] ) <= fiscal_year_end_month,
            YEAR ( [DATE] ) - 1,
            YEAR ( [DATE] )
        )
            & "/Q"
            & FORMAT (
                IF (
                    fiscal_year_end_month < MONTH ( [Date] ),
                    DATE ( YEAR ( [Date] ), MONTH ( [Date] ) - fiscal_year_end_month, 1 ),
                    DATE ( YEAR ( [Date] ) - 1, MONTH ( [Date] ) + 12 - fiscal_year_end_month, 1 )
                ),
                "Q"
            ),
        "Monthnumber", FORMAT ( [Date], "MM" ),
        "YearMonthnumber", FORMAT ( [Date], "YYYY/MM" ),
        "YearMonthShort", FORMAT ( [Date], "YYYY/mmm" ),
        "MonthNameShort", FORMAT ( [Date], "mmm" ),
        "MonthNameLong", FORMAT ( [Date], "mmmm" ),
        "DayOfWeekNumber", WEEKDAY ( [Date] ),
        "DayOfWeek", FORMAT ( [Date], "dddd" ),
        "DayOfWeekShort", FORMAT ( [Date], "dddd" )
    )
```

![Image]({{ site.url }}/images/blog/powerbi-add-a-date-table/2.JPG)

This excellent tip was posted by Power BI Community moderator Eric Zhang <a href="https://community.powerbi.com/t5/Desktop/Power-Query-M-version-of-CALENDARAUTO-DAX-function/td-p/53747">here</a>. 

If you have not added any other dataset or you have not designated a date column in one of your tables as a date, you may get this error message. You have to make sure you set the column to Date/Time.

![Image]({{ site.url }}/images/blog/powerbi-add-a-date-table/1-.JPG)

### 2) Add a New Calculated Column in DAX to your Table in Power BI

After selecting the table, select New Column in the Modeling Tab.

![Image]({{ site.url }}/images/blog/powerbi-add-a-date-table/4.JPG)

```javascript
YYYYMMDD = VALUE ( FORMAT ( Sales[OrderDate], "YYYYMMDD" ) )
```

You can add this to new column to all your tables that have a date/time column.

### 3) Create Relationship between the column we just created and the date table

Create a new relationship between the table (YYYYMMDD) and the date table (DateAsInteger). Select Many to One under Cardinality.

![Image]({{ site.url }}/images/blog/powerbi-add-a-date-table/3.JPG)

You should now be able to add any date column from the date table as a slicer. This saves you a lot of time the more datasets you add to your model and makes reporting by dates so much easier.
