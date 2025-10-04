# 🏗️ End-to-End AWS Data Pipeline (Zillow + RapidAPI + Airflow + Lambda + Redshift + QuickSight)

![Pipeline Architecture](D:\aws\Zillow Data Analytics (RapidAPI)\images\architecture diagram.drawio.png)

## 📖 Project Overview
This project demonstrates how to build a **real-time, end-to-end data pipeline** on AWS.  
Data is extracted from the **Zillow RapidAPI**, processed, transformed, and then loaded into **Amazon Redshift** for analytics and visualization using **Amazon QuickSight**.  

The pipeline leverages **Apache Airflow**, **AWS Lambda**, and **Amazon S3 buckets** to handle orchestration, transformations, and data flow across different layers.

---

## ⚙️ Architecture
1. **Extract**: Zillow data is extracted via RapidAPI using Python in **Airflow**.  
2. **Landing Zone**: Raw JSON response is stored in the first **S3 bucket**.  
3. **Intermediate Zone**: An AWS Lambda function copies the raw data to a staging bucket.  
4. **Transform**: Another Lambda function cleans/transforms the JSON → CSV (only required fields).  
5. **Transformed Zone**: The cleaned CSV is uploaded to the final S3 bucket.  
6. **Load**: Data is loaded into **Amazon Redshift** for warehousing.  
7. **Visualize**: **Amazon QuickSight** dashboards are created on top of Redshift tables.  

---

## 🛠️ Tech Stack
- **Python** (Data extraction and Airflow tasks)
- **Apache Airflow** (Orchestration on EC2)
- **AWS S3** (Landing, Intermediate, and Transformed zones)
- **AWS Lambda** (Copy + Transform logic)
- **Amazon Redshift** (Data Warehouse)
- **Amazon QuickSight** (Business Intelligence Dashboard)
- **RapidAPI (Zillow API)** (Data Source)

---

## 📂 Project Structure
