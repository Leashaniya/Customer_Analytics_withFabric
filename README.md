# Customer Analytics Platform with Microsoft Fabric (Medallion Architecture)

This repository contains an end-to-end Customer Analytics data platform built using Microsoft Fabric following the Medallion Architecture .
The project focuses on data engineering best practices: ingestion, transformation, orchestration, lineage, and analytics readiness.

### **🔗 Medium Blog (Full Walkthrough)**
📖 Read the full blog here: https://medium.com/@leashakrish2002/building-an-end-to-end-customer-analytics-platform-with-microsoft-fabric-using-medallion-53cb4734cafb?postPublishedType=repub

## 🎯 What This Project Covers
Metadata-driven ingestion using GitHub APIs

Handling large files using GitHub Releases

Bronze → Silver cleaning + standardization (Delta tables)

Silver → Gold business-ready transformations + aggregations

End-to-end orchestration using Fabric Pipelines

Built-in Fabric Task Flow + Lineage tracking

## 📦 Dataset Sources
Kaggle Dataset: Customer 360
<KAGGLE_LINK>: https://www.kaggle.com/datasets/vinaykandimalla/customer-360

### GitHub Releases (large files): orders.csv, events.csv
Pulled via GitHub API endpoints using metadata JSON.

### GitHub Main Branch (smaller files): customers.csv, products.csv, tickets.csv
Pulled via GitHub API endpoints using metadata JSON.

## 🧱 Architecture (Medallion)
### Bronze (Raw)
Stores data exactly as received

### Silver (Cleaned & Standardized)
Data cleaning (nulls, invalid formats, inconsistent strings)

Datatype corrections (dates, numeric fields)

Stored as Delta tables:

  silver_customers
  
  silver_orders
  
  silver_products
  
  silver_events
  
  silver_tickets

### Gold (Business-Ready)
Aggregations and joins across entities

Produces analytics-ready datasets (Customer-level metrics)

Stored as Delta tables in Gold lakehouse:

  gold_customer_360


### **Step 1**  Create Fabric Workspace
Create a new workspace in Fabric (Customer Analytics)

### **Step 2**  Metadata-driven Ingestion Setup (GitHub API)
Large files (GitHub Releases)

Located in: metadata/github_releases_files.json

Smaller files (Main branch)

Located in: metadata/github_main_branch_files.json

<img width="1179" height="581" alt="image" src="https://github.com/user-attachments/assets/08ce4814-33a6-4c73-8dc2-ab0a3625d6af" />

### **Step 3**  Ingest Data into Bronze (Fabric Pipeline)
Create a Fabric Data Pipeline

Use:

  Lookup to read metadata JSON
  
  ForEach to loop through file list
  
  Copy Data to pull from GitHub and store into Bronze lakehouse /Files/Dataset/
  

### **Step 4**  Bronze to Silver Transformations (Notebook)
Run the notebook:

notebooks/Bronze2Silver_CustomerAnalytics_Notebook.ipynb

Outputs:

Delta tables created in Silver lakehouse:
silver_customers

silver_orders

silver_products

silver_events

silver_tickets

### **Step 5**  Silver to Gold Transformations (Notebook)
Run the notebook:

notebooks/Silver2Gold_CustomerAnalytics_Notebook.ipynb

Creates business metrics such as:

Total customers

Revenue

Total orders

Avg order value

Engagement indicators 

### **Step 6**  End-to-End Orchestration Pipeline

Create a parent orchestration pipeline that runs in sequence:

      Invoke ingestion pipeline

      Run Silver notebook

      Run Gold notebook

<img width="1031" height="691" alt="image" src="https://github.com/user-attachments/assets/ec71a04a-20eb-4d62-aa10-98b671936d43" />


### **Step 7**  Semantic Model and Report 
A semantic model is created on top of the Gold layer for analytics.


<img width="1532" height="863" alt="image" src="https://github.com/user-attachments/assets/1d9cc50d-f72d-4dbf-a52c-0d74582cd442" />


<img width="1849" height="784" alt="image" src="https://github.com/user-attachments/assets/6f78d975-cdd3-42f1-ada7-e9745cbc8679" />
