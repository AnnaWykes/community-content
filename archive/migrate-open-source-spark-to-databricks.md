# Migrating from Open Source Apache Spark to Databricks

These instructions are designed for community leaders and presenters who wish to pick up this session on **Migrating from Open Source Apache Spark to Databricks**, and present it at community events. Below, you'll find all the necessary assets and relevant instructions for each stage of the presentation.

## Session Details

**Session Title:** Migrating from Open Source Apache Spark to Databricks

**Session Abstract:** Many organizations run Apache Spark workloads on open source distributions (such as Spark on Hadoop/YARN, standalone clusters, or cloud-managed services like EMR and HDInsight) and are looking to modernize their data engineering and analytics pipelines. In this session, we'll explore why and how to migrate these workloads to Databricks — a unified data intelligence platform built on Apache Spark. We'll cover the key differences between open source Spark and Databricks, walk through a proven migration approach, highlight common pitfalls, and demonstrate how to run your first workload on Databricks.

**Level:** 200

**Goal of the session:** Help data engineers and architects understand what's involved in migrating Spark workloads to Databricks, and give them a practical path to get started.

**Duration:** 45–60 Minutes + Q&A

**Speaker Expectation/Skills:** Speakers should have hands-on experience with Apache Spark (PySpark or Scala), familiarity with distributed computing concepts, and a basic understanding of cloud data platforms.

## Session Overview

The session covers the following topics:

- **Why migrate?** — Business drivers, cost, scalability, and the Databricks value proposition
- **Open source Spark vs. Databricks** — Key architectural differences (Delta Lake, Unity Catalog, Photon engine, MLflow integration)
- **Migration strategy** — Assessing your current workloads, choosing a migration approach (lift-and-shift vs. refactor), and planning the cutover
- **Step-by-step migration walkthrough** — Translating jobs, notebooks, and pipelines from open source Spark to Databricks
- **Common pitfalls and how to avoid them** — Configuration differences, library management, cluster sizing, and dependency handling
- **Live demo** — Running an existing PySpark batch job on Databricks Community Edition
- **What's next** — Delta Live Tables, Databricks Workflows, and the Lakehouse architecture

## Key Audience Takeaways

By the end of this session, participants will:

- Understand the architectural differences between open source Apache Spark and Databricks
- Have a clear, phased migration approach they can apply to their own workloads
- Know the most common pitfalls when migrating Spark jobs and how to avoid them
- Be able to run an existing PySpark script on Databricks with minimal code changes
- Understand how Databricks features like Delta Lake, Unity Catalog, and Workflows can improve their pipelines

## Session Key Technologies

- Apache Spark (PySpark / Scala)
- Databricks (Workspace, Notebooks, Clusters, Workflows)
- Delta Lake
- Unity Catalog
- Databricks Community Edition (free tier — great for demos)

## Prerequisites for Attendees

- Basic understanding of Apache Spark concepts (RDDs, DataFrames, Spark SQL)
- A [Databricks Community Edition account](https://community.cloud.databricks.com/login.html) (free, no credit card required) for hands-on follow-along

## Demo Overview

### Demo 1 — Running an Existing PySpark Job on Databricks

Show how a standard PySpark script that reads a CSV file, applies transformations, and writes Parquet output can be run on Databricks with minimal changes:

1. Upload the script as a Databricks Notebook or as a Python file
2. Attach a cluster and run the job
3. Highlight what changed (e.g., `SparkSession` creation is automatic, use `dbfs:/` paths instead of local/HDFS paths)

### Demo 2 — Migrating a Batch Pipeline to Delta Lake

Show how to convert a traditional Spark job that writes Parquet files into a Delta Lake table, enabling ACID transactions, schema enforcement, and time travel:

```python
# Before (open source Spark — writing Parquet)
df.write.mode("overwrite").parquet("/data/output/sales")

# After (Databricks — writing to Delta Lake)
df.write.format("delta").mode("overwrite").saveAsTable("catalog.schema.sales")
```

### Demo 3 — Scheduling a Job with Databricks Workflows

Walk through converting a cron-scheduled Spark submit job into a Databricks Workflow, showing the UI-based job scheduler and how to chain multiple tasks.

## Migration Checklist

Use this checklist to assess readiness before migrating:

- [ ] Inventory all Spark jobs (notebooks, scripts, Spark Submit commands)
- [ ] Identify external dependencies (JARs, Python packages, data sources)
- [ ] Assess data storage (HDFS, S3, ADLS, GCS) and confirm Databricks access
- [ ] Review cluster configurations and map to Databricks cluster policies
- [ ] Identify any Spark Streaming jobs and plan for migration to Structured Streaming on Databricks
- [ ] Evaluate Delta Lake adoption for existing Parquet/ORC tables
- [ ] Plan Unity Catalog data governance setup
- [ ] Run pilot migration with a non-critical workload
- [ ] Validate outputs against the original Spark environment
- [ ] Establish monitoring and alerting using Databricks observability features

## Key Differences Reference

| Feature | Open Source Spark | Databricks |
|---|---|---|
| Cluster management | Manual (YARN, Kubernetes, standalone) | Managed, auto-scaling clusters |
| Storage format | Parquet, ORC, CSV, JSON | Delta Lake (ACID, versioning) |
| Notebooks | Zeppelin, Jupyter | Databricks Notebooks (collaborative, version-controlled) |
| Data catalog | Hive Metastore (self-managed) | Unity Catalog (governed, multi-cloud) |
| Job scheduling | Oozie, Airflow, cron | Databricks Workflows |
| ML integration | MLlib + external tools | MLflow (built-in experiment tracking) |
| Performance | Spark optimizer | Photon engine (C++ vectorized) |
| Security | Self-managed | Enterprise-grade, Unity Catalog RBAC |

## Session Resources and References

- [Databricks Documentation — Migrating to Databricks](https://docs.databricks.com/en/migration/index.html)
- [Delta Lake Documentation](https://docs.delta.io/latest/index.html)
- [Databricks Community Edition (Free)](https://community.cloud.databricks.com/)
- [Unity Catalog Overview](https://docs.databricks.com/en/data-governance/unity-catalog/index.html)
- [Databricks Workflows Documentation](https://docs.databricks.com/en/workflows/index.html)
- [Apache Spark Official Documentation](https://spark.apache.org/docs/latest/)
- [Migrating Apache Spark Jobs to Azure Databricks](https://learn.microsoft.com/en-us/azure/databricks/migration/)
