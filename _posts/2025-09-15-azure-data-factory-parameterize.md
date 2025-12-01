---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: "ADF Made Dynamic with Parameters"
headline: "ADF Made Dynamic with Parameters"
tags:
- Azure Data Factory
- Data Engineering
- ETL
- Azure
categories:
  - Azure
---

When working with public datasets that publish monthly files, it’s common to see a consistent naming pattern where only the month changes. Instead of creating a different dataset for each file, Azure Data Factory makes it easy to parameterize the path and handle all variations in a single pipeline.

In this post, I’ll show how I configured an HTTP dataset to download Parquet files dynamically, using a dataset parameter and a `ForEach` loop to iterate through the months. The example uses the NYC TLC Green Taxi dataset, but the same approach works for any HTTP-based file source.

---

## 1. Adding a Dataset Parameter

Start by opening your HTTP dataset and creating a parameter that will represent the month.

- **Name:** `p_month`
- **Type:** `String`

![Parameter Screenshot]({{ site.url }}/images/blog/adf-http-parameter/0.png)

This parameter will be set by the pipeline at runtime.

---

## 2. Building the Dynamic Relative URL

Next, go to the **Connection** tab. The dataset uses a Base URL, and the Relative URL contains the file path you want to make dynamic.

In the dynamic expression builder, reference the parameter directly:

trip-data/green_tripdata_2023-0@{dataset().p_month}.parquet

yaml
Copy code

![Expression Builder Screenshot]({{ site.url }}/images/blog/adf-http-parameter/1.png)

After saving, the dataset shows the dynamic URL:

![Relative URL Screenshot]({{ site.url }}/images/blog/adf-http-parameter/2.png)

At runtime, the `p_month` value from the pipeline will be substituted into the file name.

---

## 3. Looping Through the Months with a ForEach Activity

To avoid running each month manually, add a **ForEach** activity to your pipeline.

On the **Settings** tab:

- Enable **Sequential**
- Set **Items** to: @range(1,12)


![ForEach Settings Screenshot]({{ site.url }}/images/blog/adf-http-parameter/3.png)

This expression creates a sequence of numbers from 1 to 12.

---

## 4. Passing the Parameter Value from the Copy Activity

Inside the ForEach, use a **Copy data** activity that points to the parameterized HTTP dataset. On the **Source** tab, pass the current loop value into the dataset parameter:
p_month = @item()


![Copy Activity Screenshot]({{ site.url }}/images/blog/adf-http-parameter/4.png)

`@item()` retrieves the value from the loop iteration, allowing the dataset to build the correct URL before making the GET request.

---

## Final Thoughts

By combining a parameterized dataset with a simple ForEach loop, you can cleanly ingest time-partitioned files without maintaining multiple datasets or hard-coded paths. It keeps your pipelines easier to manage and works especially well for public datasets and recurring monthly drops.

---

