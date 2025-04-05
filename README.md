## Food-Delivery-Analysis Pipeline

This project demonstrates a real-time analytics pipeline for a food delivery app using Apache Airflow, Apache Spark Structured Streaming, Amazon EMR, AWS Kinesis, Amazon S3, and Amazon Redshift. It ingests, transforms, and analyzes food delivery order data in real time to support operational dashboards and insights.


## Project Overview
The goal of this project is to build an end-to-end data pipeline capable of:

- Ingesting real-time order data using Kinesis Data Streams

- Processing streaming data with PySpark on EMR

- Persisting transformed data into Amazon Redshift

- Maintaining and loading dimension tables with Airflow DAGs

- Enabling real-time and historical analysis for food delivery insights

## Architecture
### Dimension Table Load:

- Dimension CSV files are uploaded to S3.
- Airflow loads them into Amazon Redshift using S3ToRedshiftOperator.
- Fact table is created and prepared to accept streaming data.

### Real-Time Fact Table Population:

- A Spark Structured Streaming job running on EMR reads data from AWS Kinesis.
- Transforms and writes the data to the factOrders table in Redshift using JDBC.

### Orchestration:

Airflow is used to orchestrate the workflow:
- create_and_load_dim: Creates schema and loads dimension tables.
- submit_pyspark_streaming_job_to_emr: Triggers a streaming job on EMR.

## Tech Stack
- Data Orchestration: Apache Airflow
- Stream Processing: Apache Spark Structured Streaming
- Streaming Source: AWS Kinesis
- Cloud Infrastructure: Amazon EMR, Amazon S3
- Data Warehouse: Amazon Redshift
- Programming: Python, PySpark, SQL

## Key Features
### Real-Time Data Processing:

- Utilizes Apache Spark Streaming to process food delivery data in real-time from Amazon Kinesis.
- Processes and deduplicates incoming data streams, ensuring accurate and timely order tracking.

### ETL Pipeline for Data Integration:

- Loads food delivery data from S3 into Redshift using Airflow’s S3ToRedshiftOperator.
- Automates schema creation and data insertion into dimension (dimCustomers, dimRestaurants, dimDeliveryRiders) and fact (factOrders) tables in Redshift.

### Seamless Integration with AWS Services:

- Leverages AWS Kinesis for real-time data streaming, ensuring continuous data flow for order events.
- Utilizes AWS Redshift as a data warehouse for efficient data storage and query processing.

### Data Deduplication:

- Implements stateful deduplication using Spark's watermarking feature, ensuring only unique records are processed.
- Watermarking helps in handling late-arriving data and avoiding duplicates for the same order ID.

### Automated Workflow with Airflow:

- Airflow DAGs orchestrate the ETL processes and trigger real-time data processing jobs on EMR.
- Automation of task dependencies (e.g., loading data into Redshift after schema creation) reduces manual intervention and enhances pipeline reliability.

### Scalable and Flexible Architecture:

- Scalable solution using Apache Spark on Amazon EMR for large-scale data processing.
- Easily adjustable for handling different data sources or extending to additional dimensions or metrics.

