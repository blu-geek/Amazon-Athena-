# Amazon-Athena-
Querying S3 with Amazon Athena 


<img width="724" alt="Screenshot 2025-01-11 at 18 14 34" src="https://github.com/user-attachments/assets/af031bed-8588-45d2-b664-4ad0deeee452" />


# Activity Guide: Analyzing CSV Data in S3 with Amazon Athena

1. Introduction to Amazon Athena
What is Athena?
Amazon Athena is an interactive query service for analyzing data in Amazon S3 using SQL.
Serverless: No infrastructure to manage, pay only for queries you run.

- Prereqisites:
AWS Account:Ensure you have an active AWS account (Free Tier or Paid).
Required Data:
Download the COVID-19 India dataset.

2. Create S3 Buckets:
Create a source bucket (e.g., k21-athena-source) to upload the CSV data.
Create a destination bucket (e.g., k21-athena-destination) to store Athena query results.
- Upload Data:
Create a folder named COVID in the source bucket.
Upload the downloaded raw_data1.csv file to the COVID folder.

3. Configure Amazon Athena
- Set Up Query Results Location:
In the Athena Console, go to Settings and configure the destination bucket for query results.
- Create a Table:
Use the following DDL query to define a table schema:
CREATE EXTERNAL TABLE `covid`(
  `patient number` bigint,
  `state patient number` string,
  `date announced` string,
  `age bracket` string,
  `gender` string,
  `detected city` string,
  `detected state` string,
  `current status` string,
  `notes` string
)  
ROW FORMAT DELIMITED  
FIELDS TERMINATED BY ','  
STORED AS INPUTFORMAT  
  'org.apache.hadoop.mapred.TextInputFormat'  
OUTPUTFORMAT  
  'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'  
LOCATION 's3://k21-athena-source/COVID/';

4. Query the Data:
Example query to analyze data:
SELECT count(*) FROM covid WHERE gender = 'M' AND detected_city = 'Bengaluru';

5. Clean Up Resources
Delete Athena Table:
In the Athena Console, click the three dots beside the table name and select Delete Table.
Delete S3 Buckets:
Empty and delete both the source and destination buckets to avoid additional charges.

6. Troubleshooting
Error: Query Failed
Cause: Default database not selected.
Fix: Ensure the default database is selected before running queries.

7. Summary
Successfully uploaded CSV data to S3.
Created a table and analyzed data using Amazon Athena’s SQL interface.
Cleaned up resources to minimize costs.
