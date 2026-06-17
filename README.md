*** 🚀 AWS Serverless ETL Pipeline: JSON to Parquet Data Lake

This project demonstrates an end-to-end Serverless ETL Pipeline on AWS using Amazon S3, AWS Lambda, AWS Glue, and Amazon Athena. The pipeline automatically processes raw JSON order data, transforms it into a flattened tabular format, stores it as Parquet files in a Data Lake, catalogs the data using AWS Glue, and enables SQL-based analytics through Athena.

📌 Architecture
Amazon S3 (JSON Files)
        │
        ▼
AWS Lambda (ETL Processing)
        │
        ▼
Amazon S3 (Parquet Data Lake)
        │
        ▼
AWS Glue Crawler
        │
        ▼
AWS Glue Data Catalog
        │
        ▼
Amazon Athena
🏗️ Project Overview

The objective of this project is to automate the ingestion and transformation of nested JSON order data into an analytics-ready format.

Source Data

Raw order data is uploaded in JSON format to an S3 bucket.

ETL Process

The Lambda function:

Reads JSON files from S3
Flattens nested customer and product data
Converts data into a Pandas DataFrame
Saves transformed data in Parquet format
Uploads Parquet files to a Data Lake folder
Automatically triggers a Glue Crawler
Analytics

AWS Glue creates metadata tables in the Data Catalog, allowing Athena to query the data directly from S3 using SQL.

🛠️ AWS Services Used
Service	Purpose
Amazon S3	Store raw JSON and processed Parquet files
AWS Lambda	Serverless ETL transformation
AWS Glue Crawler	Discover schema and create metadata
AWS Glue Data Catalog	Central metadata repository
Amazon Athena	Query data using SQL
IAM	Access and permission management
📂 S3 Bucket Structure
project-etl-serverless-01
│
├── orders_json_incoming/
│   ├── orders_sample_1.json
│   ├── orders_sample_2.json
│
└── orders_parquet_datalake/
    ├── orders_ETL_20260615_101500.parquet
    ├── orders_ETL_20260615_102030.parquet
⚙️ Workflow
Step 1: Upload JSON File

Upload a JSON file to:

orders_json_incoming/
Step 2: S3 Event Trigger

An S3 event notification automatically invokes the Lambda function.

Step 3: Lambda Transformation

The Lambda function:

Reads JSON file
Extracts customer details
Extracts product details
Flattens nested structures
Converts data into tabular format

Example Output:

order_id	customer_name	product_name	quantity
1001	John Doe	Laptop	1
1001	John Doe	Mouse	2
Step 4: Convert to Parquet

The transformed DataFrame is saved as:

df.to_parquet()

Output Location:

orders_parquet_datalake/
Step 5: Trigger Glue Crawler

Lambda automatically starts:

glue.start_crawler()

The crawler:

Scans Parquet files
Detects schema
Creates or updates tables
Updates Glue Data Catalog
Step 6: Query Using Athena

Run SQL queries directly on S3 data.

Example:

SELECT
    category,
    COUNT(*) AS total_orders,
    SUM(total_amount) AS total_sales
FROM orders
GROUP BY category
ORDER BY total_sales DESC;
💡 Why Parquet?

Parquet is a columnar storage format optimized for analytics workloads.

Benefits

✅ Faster query performance

✅ Reduced storage cost

✅ High compression ratio

✅ Better analytics performance

✅ Lower Athena query costs

Athena charges based on data scanned. Since Parquet stores only required columns, less data is scanned compared to JSON files.

📊 Sample Athena Output
Category	Total Orders	Total Sales
Electronics	120	24,500
Clothing	95	12,700
Books	80	7,300
🔐 IAM Permissions Required
Lambda Role
AmazonS3FullAccess
AWSGlueConsoleFullAccess
Glue Role
AWSGlueServiceRole
AmazonS3ReadOnlyAccess
📈 Key Learnings
Event-Driven Architecture
Serverless Data Engineering
AWS Lambda Automation
Data Lake Concepts
Glue Data Catalog Management
Athena Query Optimization
JSON to Parquet Transformation
Cloud-Based Analytics
🚀 Future Enhancements
Add data validation checks
Partition Parquet files by date
Use AWS Step Functions for orchestration
Integrate Amazon QuickSight for dashboards
Implement CI/CD deployment pipeline
Add monitoring using CloudWatch
📷 Architecture Diagram

Add your architecture image here:

![Architecture](images/aws-serverless-etl-pipeline.png)
👨‍💻 Author

Akash Kokne

🔹 Data Analyst | Power BI | SQL | Python | AWS Cloud Practitioner
🔹 Exploring Data Engineering & Cloud Analytics

📫 Connect with me on LinkedIn and feel free to share feedback or suggestions!
