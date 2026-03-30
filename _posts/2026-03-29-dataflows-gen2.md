---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: "Dataflows Gen2 in Microsoft Fabric"
headline: "Dataflows Gen2 in Microsoft Fabric"
tags:
- Azure
- Data Engineering
- Fabric
- Power BI
categories:
  - Azure
  - Data Engineering
  - Fabric
---

If you have been using Power BI dataflows for data prep and ETL, Dataflows Gen2 in Microsoft Fabric is the next step. It keeps everything you already know from Power Query but adds proper data destinations, pipeline integration, better monitoring, and high-performance compute. This post covers what changed, what stayed the same, and what you need to know to start using Gen2.

![Dataflows Gen2]({{ site.url }}/images/blog/dataflows-gen2.png)

---

## What Gen1 Was

Power BI Dataflows (Gen1) let you connect to data sources, clean and reshape data using Power Query, and store the results so Power BI reports could connect to them through the Dataflow connector. The idea was solid: one place to prepare data, reused across many reports, with scheduled refresh to keep it current.

The limitation was always the destination. Gen1 stored data in its own internal storage or optionally in your own Azure Data Lake (BYOL). That was it. You couldn't push directly to a Lakehouse, Warehouse, or Azure SQL. And there was no way to hook a dataflow into a pipeline alongside other activities.

Gen2 fixes both of those things.

---

## What Is New in Gen2

### Multiple Output Destinations

This is the biggest change. Instead of writing to internal storage only, Gen2 lets each query in a dataflow write to its own destination. You can mix destinations within the same dataflow. Supported targets include:

- Fabric Lakehouse (Tables or Files)
- Fabric Warehouse
- Fabric KQL Database
- Fabric SQL Database
- Azure SQL Database
- Azure Data Lake Gen2
- Azure Data Explorer
- Snowflake
- SharePoint Files

This means your dataflow can clean data and load it straight into a Lakehouse table or Warehouse without any extra steps. No pipelines just to move the output somewhere useful.

### Pipeline Integration

Gen2 works as an activity inside Data Factory Pipelines. You can chain it with copy activities, stored procedures, notebooks, and more on a unified schedule. Gen1 had no pipeline support at all.

### AutoSave and Background Publishing

Gen2 saves your work automatically as you go. When you publish, validation runs in the background and you don't have to wait for it to finish before moving on.

### High-Performance Compute

Gen2 uses Fabric SQL Compute engines for handling large data efficiently. When you first create a dataflow in a workspace, Fabric automatically creates a staging Lakehouse and Warehouse (named `DataflowStaging...`). These are shared across all dataflows in the workspace and handle the compute. Do not delete them.

### Copilot

Gen2 integrates with Copilot in Fabric. You can use natural language to apply transformations:

- "Only keep European customers"
- "Count the total number of employees by City"
- "Only keep orders whose quantities are above the median value"

Each prompt gets applied as a step in the Applied Steps list. Type "Undo" to remove the last step.

### Recent Data Sources

Gen2 tracks previously used sources so you can reload them directly without reconfiguring connections each time.

---

## Feature Comparison

<table align="center">
  <thead>
    <tr>
      <th>Feature</th>
      <th>Gen2</th>
      <th>Gen1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Power Query authoring</td>
      <td>Yes</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Multiple output destinations</td>
      <td>Yes</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Pipeline integration</td>
      <td>Yes</td>
      <td>No</td>
    </tr>
    <tr>
      <td>AutoSave and background publish</td>
      <td>Yes</td>
      <td>No</td>
    </tr>
    <tr>
      <td>High-performance Fabric compute</td>
      <td>Yes</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Copilot / natural language authoring</td>
      <td>Yes</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Monitoring Hub integration</td>
      <td>Yes</td>
      <td>No</td>
    </tr>
    <tr>
      <td>Incremental refresh</td>
      <td>Yes</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>DirectQuery via Dataflow connector</td>
      <td>No</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>Bring your own lake (BYOL)</td>
      <td>No</td>
      <td>Yes</td>
    </tr>
    <tr>
      <td>CDM folders</td>
      <td>No</td>
      <td>Yes</td>
    </tr>
  </tbody>
</table>

One thing to flag: Gen2 does not support DirectQuery through the Dataflow connector. The replacement is to use data destinations and connect your reports directly to the output table in the Lakehouse or Warehouse.

---

## How to Create a Dataflow Gen2

### 1. Create the Dataflow

Open your Fabric workspace, select **+ New item**, then select **Dataflow Gen2**.

![New Dataflow Gen2]({{ site.url }}/images/blog/dataflows-gen2/1.png)

### 2. Get Data

Select **Get data**, choose your source, configure the connection, and select the tables or files you want to work with.

![Get Data]({{ site.url }}/images/blog/dataflows-gen2/2.png)

### 3. Transform in Power Query

The editor is the same Power Query experience from Excel and Power BI Desktop. A few things worth enabling before you start:

- **Data Profiling**: Go to **Home > Options > Global Options** and enable column profiling to see column quality and distribution.
- **Diagram View**: Useful for visualising query dependencies, especially when merging or referencing multiple queries.

![Power Query Editor]({{ site.url }}/images/blog/dataflows-gen2/3.png)

### 4. Set a Data Destination

In the **Query settings** pane, scroll to the bottom and select **Choose data destination**. Pick your target (Lakehouse, Warehouse, Azure SQL, etc.), connect, and configure the update method.

Two update methods are available:

- **Replace**: Full refresh on every run. The table is dropped and recreated.
- **Append**: New rows are added to the existing table on each refresh.

For the Replace method, you can choose between:

- **Dynamic schema**: Handles schema changes automatically but drops and recreates the table each time. Relationships and measures on the table may be removed.
- **Fixed schema**: Preserves relationships and measures. The schema cannot change. Use this when you have reports or models built on top of the destination table.

![Data Destination]({{ site.url }}/images/blog/dataflows-gen2/4.png)

### 5. Publish

Select **Publish** in the lower right. The first time you publish in a workspace, Fabric creates the `DataflowStaging` Lakehouse and Warehouse in the background. Leave these alone.

---

## Migrating from Gen1 to Gen2

There are three ways to move Gen1 dataflows across.

### Export Template (recommended for full dataflows)

1. Open the Gen1 dataflow and select **Home > Export template**
2. Save the `.pqt` file
3. Create a new Dataflow Gen2 in your Fabric workspace
4. Select **Import from a Power Query template** and open the `.pqt` file
5. Reconnect credentials when prompted

### Copy and Paste (recommended for partial migrations)

1. Open the Gen1 dataflow in Power Query
2. Select the queries you want (Ctrl+click for multiple), then Ctrl+C
3. Open a Dataflow Gen2, add a blank query, then Ctrl+V to paste
4. Delete the blank query and reconnect credentials

### Save As (fastest for full conversion)

1. In the workspace, select **...** next to the Gen1 dataflow
2. Select **Save as Dataflow Gen2**
3. Review and publish

Note: scheduled refresh settings are not carried over by any of these methods. Reconfigure refresh after migrating.

---

## Things to Know Before You Start

**The `DataflowStaging` items must not be deleted.** Fabric creates these automatically in your workspace and uses them for compute across all your Gen2 dataflows. Deleting them will break your dataflows.

**Warehouse destinations require staging.** If you want to write to a Fabric Warehouse, staging must be enabled on the queries. Warehouse loading also only supports the same workspace as the dataflow.

**Nullable column errors.** If Power Query detects a column as non-nullable but the source data contains nulls, the refresh will fail when writing to a destination. Fix it by setting the data type explicitly in Power Query using `type nullable text` or `type nullable Int64.Type`.

**Vacuum your Lakehouse tables regularly.** Delta tables accumulate old files over time. Run Maintenance > Vacuum on Lakehouse destination tables to clean up unreferenced files. Keep the retention at 7 days minimum. If you are using incremental refresh on a table, turn off vacuuming for that table as it can interfere with the process.

**Fixed schema for Warehouse and Snowflake.** Both require fixed schema, so you cannot use dynamic schema with these destinations.

---

## Final Thoughts

Gen2 is a meaningful upgrade from Gen1, not just a rename. The combination of flexible data destinations and pipeline integration removes the friction that made Gen1 feel limited outside of pure Power BI use cases. If you are starting something new in Fabric, use Gen2. If you have existing Gen1 dataflows, the migration tools are straightforward and the Export Template approach makes it easy to move without losing your transformation logic.

The one gap to plan for is DirectQuery. If your current reports rely on DirectQuery through the Dataflow connector, you will need to rebuild those connections against the destination table after migrating.

---
