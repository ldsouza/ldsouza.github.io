---
layout: post
published: true
mathjax: false
featured: false
comments: false
title: "Moving from Azure Synapse Analytics to Microsoft Fabric"
headline: "Moving from Azure Synapse Analytics to Microsoft Fabric"
tags:
- Azure
- Data Engineering
- Fabric
categories:
  - Azure
  - Data Engineering
  - Fabric
---

If you've been building on Azure Synapse Analytics and are starting to look at Microsoft Fabric, the hardest part isn't the technology. It's figuring out what maps to what. Fabric doesn't just replace Synapse. It reorganizes the pieces, renames some of them, and adds capabilities that didn't exist before. Once you understand the equivalencies, the path forward is a lot clearer.

![Moving from Azure Synapse to Microsoft Fabric]({{ site.url }}/images/blog/moving-from-azure-synapse-to-fabric.png)

This post walks through how each part of a Synapse environment maps to Fabric, what actually changed, and what to keep in mind as you migrate.

---

## Why Fabric Instead of Synapse

Microsoft is not deprecating Synapse, but Fabric is where the investment is going. New features, new integrations, and the roadmap are all Fabric-first. Synapse will continue to work, but if you're building something new or planning a major revision, Fabric is the better long-term foundation.

Fabric also consolidates things that used to require multiple services. Power BI, data engineering, data science, real-time analytics, and data warehousing all live inside one product with a shared storage layer (OneLake) and a unified billing model (capacity units). That's a meaningful reduction in surface area compared to managing Synapse alongside standalone Power BI, Azure Data Factory, and ADLS Gen2.

---

## The Core Mapping

Here's how the main Synapse components map to Fabric:

<table align="center">
  <thead>
    <tr>
      <th>Azure Synapse</th>
      <th>Microsoft Fabric</th>
      <th>Notes</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Synapse Workspace</td>
      <td>Fabric Workspace</td>
      <td>Organizational container for items</td>
    </tr>
    <tr>
      <td>Dedicated SQL Pool</td>
      <td>Data Warehouse</td>
      <td>T-SQL, columnar storage, separate compute</td>
    </tr>
    <tr>
      <td>Serverless SQL Pool</td>
      <td>SQL Analytics Endpoint</td>
      <td>Auto-generated on every lakehouse</td>
    </tr>
    <tr>
      <td>Apache Spark Pool</td>
      <td>Spark in Fabric Notebooks</td>
      <td>PySpark, Scala, SparkSQL supported</td>
    </tr>
    <tr>
      <td>Synapse Pipelines</td>
      <td>Data Pipeline</td>
      <td>Same ADF-based engine, same activity types</td>
    </tr>
    <tr>
      <td>Synapse Link</td>
      <td>Mirroring</td>
      <td>Near real-time replication into OneLake</td>
    </tr>
    <tr>
      <td>Azure Data Lake Storage Gen2</td>
      <td>OneLake (via Shortcuts)</td>
      <td>Existing ADLS can be referenced without moving data</td>
    </tr>
    <tr>
      <td>Synapse Studio</td>
      <td>Fabric Portal</td>
      <td>Browser-based, workspace-scoped</td>
    </tr>
  </tbody>
</table>

---

## Dedicated SQL Pool to Fabric Data Warehouse

This is the closest one-to-one mapping. Fabric's Data Warehouse uses T-SQL, supports familiar DDL and DML, and stores data in columnar format. If you've been writing SQL against a dedicated pool, most of it will run as-is in Fabric.

A few differences worth knowing:

- Fabric Warehouse is built on Delta Parquet and stores data in OneLake. The underlying files are accessible directly, which wasn't the case with Synapse's dedicated pools.
- Polybase and external tables work differently. In Fabric, you use shortcuts to reference external data rather than defining external data sources and file formats separately.

If your dedicated pool has heavy use of materialized views, workload management groups, or result-set caching, check those features specifically. Coverage isn't identical.

---

## Serverless SQL Pool to SQL Analytics Endpoint

This is where Fabric takes a different approach. In Synapse, the serverless pool was a separate resource you pointed at ADLS. In Fabric, every lakehouse automatically gets a SQL analytics endpoint. You don't provision it or configure it. It's just there.

The endpoint surfaces all Delta tables in the lakehouse's Tables folder as SQL views. You query them with T-SQL. It's read-only by default, which matches the serverless pool's typical read pattern.

If you were using the serverless pool to query parquet files in ADLS, you can recreate this in Fabric by creating an ADLS shortcut in the lakehouse Files folder, loading it into Delta with a notebook, and querying through the endpoint. Or you can shortcut directly at the Tables level if the source is already Delta format.

---

## Spark Pool to Fabric Notebooks

Spark in Fabric works the same way you'd expect if you've used Synapse notebooks. PySpark, Scala, and Spark SQL are all supported. The main differences are in how you configure compute and how you reference data.

**Compute:** Synapse Spark pools are explicitly provisioned with a node size and min/max node count. In Fabric, Spark compute is provided by the capacity attached to the workspace. You configure starter pool settings (node size, autoscale range) at the workspace level under Spark settings, but you're not managing a separate pool resource.

**Data access:** In Synapse, reading from ADLS required setting up linked services and mounting storage. In Fabric, data in OneLake is natively accessible from any notebook in the workspace. To read a lakehouse table:

```python
df = spark.read.format("delta").load("Tables/my_table")
```

Or using the shorthand that Fabric notebooks support:

```python
df = spark.sql("SELECT * FROM my_lakehouse.my_table")
```

No credentials, no mount points, no linked services needed for data that lives in OneLake.

---

## Synapse Pipelines to Fabric Data Pipelines

This is the most seamless transition. Fabric Data Pipelines use the same Azure Data Factory engine that Synapse Pipelines are built on. Activities, triggers, control flow logic, and expressions work the same way. If you've built pipelines in Synapse, the authoring experience in Fabric will be familiar.

The main gap is that Fabric Pipelines don't have full feature parity with ADF yet. Integration runtimes, custom activity types, and some connector configurations may require checking before migrating complex pipelines.

For new pipelines, Fabric is the right place to build them. For existing Synapse pipelines, export the JSON definitions and import them into Fabric. Most will work without changes. Test anything with custom linked services or integration runtime dependencies.

---

## Synapse Link to Mirroring

Synapse Link was a near-real-time replication feature that brought operational data from Azure SQL, Cosmos DB, and Dataverse into Synapse without impacting the source database. Fabric Mirroring is the equivalent, and it covers more sources.

Mirroring in Fabric supports:
- Azure SQL Database
- Azure Cosmos DB
- Azure SQL Managed Instance
- Snowflake
- Azure Databricks (Unity Catalog)

The setup is straightforward: you create a mirrored database item in Fabric, connect it to the source, and Fabric replicates the data into OneLake continuously. Once it's there, you can query it from the SQL analytics endpoint or use it in notebooks, just like any other lakehouse data.

If you were using Synapse Link for Cosmos DB or Azure SQL, Mirroring is the direct replacement.

---

## Storage: ADLS Gen2 to OneLake

OneLake is Fabric's unified storage layer, built on ADLS Gen2 underneath. Every workspace gets OneLake automatically, and all Fabric items (lakehouses, warehouses, KQL databases) store their data there.

If you have existing data in ADLS Gen2 that you don't want to move, you don't have to. Create a shortcut in a Fabric lakehouse pointing to the ADLS container. The data stays where it is, and Fabric reads it directly. No egress costs, no duplication, no pipelines needed just to make the data accessible.

For a longer-term migration, you can use a notebook or Data Pipeline to copy data from ADLS into OneLake in Delta format, then drop the shortcut once the migration is complete.

---

## What Doesn't Have a Direct Equivalent

A few Synapse features don't map cleanly to Fabric today:

**Dedicated SQL Pool history and snapshots:** Synapse dedicated pools support user-defined restore points and geo-backup. Fabric Warehouse doesn't have the same snapshot-based recovery model.

**Workload management:** Synapse's workload groups and classifiers for query prioritization don't exist in Fabric Warehouse. Fabric handles this at the capacity level.

**Integration Runtime (self-hosted):** Fabric has the on-premises data gateway for connecting to on-premises sources, but it's not the same as ADF's self-hosted IR. Some connector scenarios need validation before assuming they'll work.

**Synapse ML:** If you were using SynapseML (the Spark ML library integrated into Synapse), it's available in Fabric notebooks as well, but check the specific version compatibility.

---

## Final Thoughts

Moving from Synapse to Fabric is more of a reorganization than a rebuild. The SQL skills carry over, the Spark code carries over, and the pipeline logic carries over. What changes is the structure: everything shares a storage layer, items live in workspaces rather than being scattered across services, and provisioning is simpler.

The biggest practical step is mapping your existing architecture to the Fabric equivalents, identifying what can be migrated as-is and what needs rework. For most Synapse environments, the dedicated pool to Fabric Warehouse and Spark notebooks migrations will be the bulk of the work. Pipelines and ADLS data can usually be transitioned with less effort.

If you're starting from scratch, Fabric is the right choice. If you have an existing Synapse environment, the migration is worth planning now rather than waiting until the gap between Synapse's roadmap and Fabric's capabilities gets wider.

---
