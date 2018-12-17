---
layout: post
published: true
mathjax: false
featured: false
comments: true
title: How to add a Date Table to Power BI
headline: How to add a Date Table to Power BI
tags:
- Power BI
- Data Modeling
- Reporting
categories:
  - Power BI
---

Power BI Desktop is a powerful data exploration and reporting tool that can be used to import data into the Power BI data model from several data sources. Once you have imported data from multiple sources, you can create relationships between the tables and visualize data on dashboards and reports. 

You may have a date timestamp for each one of the data sources that your import into Power BI. Instead of having multiple filters and/or slicers pulling these different date columns, a better approach is to use a date table or a date dimension from a warehouse instead. If you do not have an existing date table in a database or a warehouse somewhere, you can add one in Power BI itself.

![Image]({{ site.url }}/images/blog/powerbi-add-a-date-table/0.JPG)

There are several ways to do this

### 1) Create a Date Table in Power BI Using DAX 

This question was posted on the Power BI community page <a href="https://community.powerbi.com/t5/Desktop/Power-Query-M-version-of-CALENDARAUTO-DAX-function/td-p/53747">here</a> and moderator Eric Zhang posted an excellent solution. 

Select the Modeling Tab in Power BI Desktop and select New Table. Paste in the DAX code below and click Enter.



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

YYYYMMDD = VALUE ( FORMAT ( JSA[DatePerformed], "YYYYMMDD" ) )



SWITCH(Table1[MonthNumber],1,"January",2,"February",3,"March",4,"April",5,"May",6,"June",7,"July",8,"August",9,"September",10,"October",11,"November",12,"December")
