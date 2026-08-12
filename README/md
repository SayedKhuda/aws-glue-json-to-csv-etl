# AWS Glue JSON to CSV ETL Pipeline

## Project Overview

This project demonstrates a simple ETL (Extract, Transform, Load) pipeline using **Amazon S3** and **AWS Glue Visual ETL**.

The objective was to read employee data stored in JSON format from an Amazon S3 bucket, transform the data using AWS Glue, and save the processed data as CSV in a separate S3 bucket.

## Architecture

![AWS Glue ETL Architecture](architecture/json-to-csv-architecture.png)

### Data Flow

```text
Amazon S3 (JSON)
        ↓
AWS Glue Visual ETL
        ↓
Drop Duplicates
        ↓
Select Fields
        ↓
Amazon S3 (CSV)
```

## AWS Services Used

* **Amazon S3** – stores the source JSON data and processed CSV output.
* **AWS Glue** – performs the ETL processing.
* **AWS Glue Visual ETL** – provides the visual interface for building the data pipeline.
* **AWS IAM** – provides the permissions required for AWS Glue to access the S3 buckets.

## Source Data

The source employee dataset contains the following fields:

* `emp_id`
* `name`
* `salary`
* `address`
* `loc`
* `email`

The source data also contains duplicate employee records, allowing the pipeline to demonstrate data cleaning.

## ETL Process

### 1. Extract

The employee JSON file is stored in an Amazon S3 source bucket.

AWS Glue reads the JSON data directly from this S3 location.

### 2. Drop Duplicates

The **Drop Duplicates** transformation removes repeated employee records from the dataset.

The original dataset contains 12 records representing 6 employees twice. After the transformation, only the 6 unique employee records remain.

### 3. Select Fields

The **Select Fields** transformation keeps only the fields required for the final dataset:

```text
emp_id
name
salary
address
```

The unused `loc` and `email` fields are removed.

### 4. Load

The transformed data is written to a separate Amazon S3 destination bucket in CSV format.

The final output contains cleaned employee data with duplicate records removed and only the required columns retained.

## Output

Example transformed output:

```csv
emp_id,name,salary,address
6,rahul,0,india
1,manish,10000,india
2,rani,20000,usa
3,rinku,55000,india
5,,20000,usa
4,neha,12000,usa
```

The ordering of records may vary because the Glue `Drop Duplicates` operation does not guarantee a specific row order.

## Handling Spark Output Partitions

AWS Glue uses Apache Spark for distributed data processing. By default, Spark can create multiple output part files.

For this small dataset, I used:

```python
coalesce(1)
```

to reduce the transformed data to a single partition before writing it to Amazon S3.

## Project Screenshots

### Source Data in Amazon S3

![S3 Source](screenshots/01-source-s3.png)

### Source JSON Data

![JSON Data](screenshots/02-source-json.png)

### Successful AWS Glue Job

![Glue Job Success](screenshots/03-glue-job-success.png)

### Processed Data in Destination S3 Bucket

![S3 Output](screenshots/04-output-s3.png)

### Final Output

![Output Result](screenshots/05-output-result.png)

## Key Learning Outcomes

Through this project, I gained practical experience with:

* Creating source and destination S3 buckets
* Reading JSON data from Amazon S3
* Building an AWS Glue Visual ETL pipeline
* Removing duplicate records
* Selecting required fields
* Converting JSON data into CSV
* Understanding Apache Spark partitions
* Using `coalesce(1)` to control output partitions
* Writing transformed data back to Amazon S3
* Using IAM roles to provide AWS Glue with access to S3
* Monitoring AWS Glue job runs

## Repository Structure

```text
aws-glue-json-to-csv-etl/
├── README.md
├── data/
│   └── emp_json.json
├── architecture/
│   ├── json-to-csv-architecture.png
│   └── JSON-to-CSV.drawio
├── screenshots/
│   ├── 01-source-s3.png
│   ├── 02-source-json.png
│   ├── 03-glue-job-success.png
│   ├── 04-output-s3.png
│   └── 05-output-result.png
└── scripts/
    └── glue_etl.py
```
