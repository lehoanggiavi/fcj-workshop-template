---
title: "Blog 3 - Running Serverless Apache Spark with Amazon Athena"
date: 2026-04-19
weight: 3
chapter: false
pre: " <b> 3.3. </b> "
---

# [AWS Knowledge Sharing] Running Serverless Apache Spark with Amazon Athena – No Cluster Management Required

Hello everyone in the AWS Study Group VN community.

I recently read a very useful article from the AWS Big Data Blog about the **Apache Spark engine in Amazon Athena**. The key highlight is that we can now run Spark in a fully serverless way, without provisioning or managing EMR or Spark Clusters as before.

## The problem

When using Spark in the traditional way, Data teams often need to:

- Manage EC2, networking, and Spark Cluster configuration.
- Wait for the cluster to start before running jobs.
- Pay costs even when the cluster is idle.
- Struggle to support multiple needs at the same time, such as Notebooks, ETL Pipelines, and data analysis.

This increases operational costs and slows down data analysis.

## The solution

AWS introduces **Apache Spark Engine in Amazon Athena**, providing a fully serverless Spark environment.

Instead of managing clusters, users only need to:

- Create a Spark Session.
- Connect through Spark Connect.
- Run Spark code using familiar tools such as Jupyter Notebook, VS Code, or Apache Airflow + dbt.

Athena automatically provisions resources, scales when needed, and releases resources after completion.

## Architecture

The architecture is quite simple:

- **Amazon Athena for Apache Spark** acts as the Spark Engine.
- **AWS Glue Data Catalog** manages metadata.
- Data is stored on **Amazon S3**.
- Users can connect from Jupyter Notebook, VS Code, or Apache Airflow through Spark Connect.
- If deployment in a private environment is required, **Amazon MWAA (Managed Airflow)** can be combined with VPC Endpoint for secure connectivity.

## Notable new features

The new version of Athena for Spark adds many useful features:

- **Spark Connect** enables secure connections from external tools.
- Faster Spark Session startup, significantly reducing waiting time.
- **Live Spark UI** supports job monitoring and debugging.
- **Session-level Cost Attribution** helps track cost by individual session.
- Integration with **AWS Lake Formation** for data access management.

## Usage patterns

AWS introduces three common deployment patterns:

- **Jupyter Notebook:** suitable for Data Scientists performing data exploration and Feature Engineering.
- **VS Code:** supports coding and testing Spark applications in a familiar IDE.
- **Apache Airflow + dbt:** builds automated ETL pipelines and manages scheduled workflows.

## What I find interesting

The most impressive point to me is that Spark is no longer tied to cluster management.

We only need to focus on writing Spark code, while Athena automatically:

- Starts a Spark Session in a few seconds.
- Auto Scales based on workload.
- Charges by usage time instead of requiring a cluster to run 24/7.

This is a very worthwhile option for data analytics, ETL, or Machine Learning workloads with irregular traffic.

In my opinion, **Athena for Apache Spark** is a step forward that helps Data teams significantly reduce operational costs and infrastructure management time, while still taking advantage of the full AWS ecosystem such as S3, Glue Data Catalog, Lake Formation, and Airflow. If you are building a Data Lake or Data Platform on AWS, this is a service worth trying.
