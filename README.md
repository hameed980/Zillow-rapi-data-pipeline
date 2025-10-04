## End-to-End AWS Data Pipeline (Zillow + RapidAPI + Airflow + Lambda + Redshift + QuickSight)

## Project architecture

![Pipeline Architecture](https://github.com/user-attachments/assets/7b544852-659d-4d24-ac38-c4ea598eccf2)


### Project Overview


--- This project demonstrates how to build an end-to-end data pipeline on AWS.

We extract real estate data from the Zillow RapidAPI, process and transform it with AWS Lambda, orchestrate workflows using Apache Airflow, and load the cleaned data into Amazon Redshift. Finally, we visualize insights through Amazon QuickSight dashboards.

The architecture follows a multi-zone S3 design (Landing → Intermediate → Transformed) to separate raw, staged, and cleaned data layers.

⚙️ Architecture Workflow

Extract: Zillow data is fetched via RapidAPI using a Python script scheduled in Apache Airflow.

Landing Zone (Raw Data): Raw JSON response is stored in the first S3 bucket.

Intermediate Zone (Staging): A Lambda function copies raw files into a staging bucket.

Transform: Another Lambda function cleans and transforms JSON → CSV with only required fields.

Transformed Zone: The cleaned CSV is uploaded into the final S3 bucket.

Load: Transformed data is ingested into Amazon Redshift.

Visualize: Amazon QuickSight dashboards provide property insights (price, rent, bedrooms, etc.).

### Tech Stack

Python (Data extraction & transformations)

Apache Airflow (on EC2) – Orchestration

Amazon S3 – Landing, Intermediate, and Transformed zones

AWS Lambda – Copy + Transform functions

Amazon Redshift – Data Warehouse

Amazon QuickSight – BI & Visualization

RapidAPI (Zillow API) – Data Source

#### Outcomes

Designed and deployed a production-style AWS pipeline.

Built a scalable, serverless data architecture using S3 + Lambda.

Automated end-to-end pipeline execution with Airflow DAGs.

Transformed unstructured API JSON → structured CSV ready for analytics.

Created QuickSight dashboards for real estate trends (e.g., avg price per city, rent vs. sale prices, home types).

### Challenges & Solutions

Nested JSON Structure

Problem: API returned deeply nested JSON with unused fields.

Solution: Lambda script flattened the JSON and kept only relevant attributes (bathrooms, bedrooms, city, homeStatus, homeType, livingArea, price, rentZestimate, zipcode).

Lambda Trigger Race Condition

Problem: Lambda triggered before file upload completed in S3, causing empty reads.

Solution: Added object_exists waiter to ensure file was available before processing.

Airflow AWS Connection Issue

Problem: Airflow UI didn’t show Access/Secret Key fields.

Solution: Configured AWS credentials via environment variables and used them in Airflow connections.

QuickSight Dataset Refresh

Problem: QuickSight dashboards didn’t reflect latest Redshift updates.

Solution: Enabled auto-refresh and manual sync of datasets.

Multi-bucket Management Confusion

Problem: Mixing up Landing, Staging, and Transformed zones.

Solution: Followed naming convention project-landing, project-staging, project-transformed and documented clearly.

#### Sample Dashboard

![alt text](image.png)

#### How to Run

Clone this repository

Configure your AWS credentials (IAM role or Access Keys)

Deploy Airflow DAGs on an EC2 instance

Set up three S3 buckets (Landing, Staging, Transformed)

Deploy AWS Lambda functions for copy + transform steps

Create Redshift cluster and copy transformed data

Connect QuickSight to Redshift and build dashboards

#### Key Learning

This project helped me learn how to:

Design production-ready AWS pipelines

Handle multi-zone S3 data lakes

Integrate Airflow, Lambda, Redshift, and QuickSight end-to-end

Debug orchestration + cloud resource issues in real workflows

🔗 This project is part of my Data Engineering portfolio. Feel free to fork, explore, and share feedback!
