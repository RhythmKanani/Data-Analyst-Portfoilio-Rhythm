### Project 1 

# **Data Analytical Platform For City Of Vancouver - Rental Business Licenses.**

## 1. Objective:
-  To design and implement a secure, cloud-based data analytical platform using AWS services that enables efficient ingestion, transformation, cataloging, summarization, and analysis of business license data—focusing on Rental Services in the City of Vancouver. The goal of this Analysis was to derive insights to support employment planning and revenue tracking.

## 2. Dataset:
- Source: City of vancouver open data portal
- Sector: Rental Services
- Format: CSV
- Data: The Rental Business License dataset of City of Vancouver Included the following Key columns.
  1. License Number
  2. License Revision Number
  3. Business Name
  4. Business Trade name
  5. Status
  6. Issuedate
  7. Expireddate
  8. Business Type
  9. City
  10. Province
  11. Number of Employees
  12. Fees Paid
  13. Extract Date
  14. Geom
  15. Geo Point 2D

## 3. Methodology:
### Data Ingestion:
- Downloaded business licenses dataset from the Vancouver open data portal and Uploaded dataset to: s3://business-raw-rhy/Licenses/Rental-List/Year=2025/Server=BLGVS-RHY/
- Organized folders by year and source for raw storage
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/image.png?raw=true)
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/2.png?raw=true)

### Data Profiling and Cleaning:
- Created Transform Bucket list Business-trf-rhy and subfolders in the S3 so that clean dataset can be stored for system and users. 
- Created a project in AWS Glue DataBrew.
- Faced issue while creating the project for data profiling and connecting to new dataset because of csv delimiter. I solved this issue by changing the delimiter type to semi colon  from commas.
- Created profiling and cleaning project on Glue Databrew and run the project so that data issues can be configured through creating job and running Job profile to normalize the dataset. (bus-rental-list-prj-rhy).
- Removed unnecassary fields (geom, postal code, street, etc.)
- Replaced null values with NA, median, or most frequent value respective of the data issues present.
- Applied regex on Business Name to clean special characters
- Filled the missing values with median in feespaid, missing values with most frequent value in issue date, expired date, Country, province. Standardized date formats to YYYY-MM-DD.
- Transformed and created a clean dataset in csv & parquet format for user and system perspective and stored it in new S3 bucket called as Business-trf-rhy.
 ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/3.png?raw=true)
 ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/4.png?raw=true)
 ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/5.png?raw=true)
### Data Cataloging:
- Used AWS Glue Crawler to scan and catalog the transformed dataset
- Created a database: business-data-catalog-rhy and Generated structured tables with metadata.
 ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/6.png?raw=true)
 ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/7.png?raw=true)

### Data Summarization:
- Built Visual ETL Pipeline in Glue to:
Aggregate total fees paid
Calculate average number of employees
Group by license status
- Designed visual ETL pipeline Steps by using various summarisation features.
- Implemented Data summarisation techniques like change schema to drop and change columns, filtered province columns to target Vancouver city, used aggregate function for getting Sum total fees paid and avg number of employees, attached new column for date. These steps help to achieve the information related to Type of status, number of businesses, Sum fees paid and Average number of employees which can be used for Data analysis.
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/8.png?raw=true)
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/9.png?raw=true)
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/10.png?raw=true)
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/11.png?raw=true)

### Data Analysis:
- Used AWS Athena to answer 2 business questions:
  1. Employment Rate: What is the city-wise average number of employees in rental businesses?
  2. Revenue: How much revenue was generated through rental licenses by city in 2024?
- Used the SQL services inbuilt in Athena to answer the Business Queries mentioned above.
- For the first business query to answer and know the city wise avg no of employees to evaluate the employment rate and target job roles, DML commands such as SELECT, FROM, AS, GROUP were established by using the city and no of employee rows to derive the Avg_citywise_employees by running the query.
- Secondly, for deriving a business solution for the second business question that is Revenue generated through rental business licenses grouped by city for the year 2024. A DML command was run where the table of cities was SELECTED and by doing SUM of the fees paid for the year 2024 using WHERE and CAST function and GROUPING by city.
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/12.png?raw=true)
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/13.png?raw=true)

### Data Security:
- Configured custom KMS key (rental-licenses-key-rhy) for the purpose of providing confidentiality & integrity protection layer for the data analytical platform for datasets in the S3 Buckets.
- Applied key for encryption on all buckets
- Enabled bucket versioning for recovery
- Created replication rules to back up:
  1. Raw: business-raw-bac-rhy
  2. Transformed: business-trf-bac-rhy
  3. Curated: business-cur-bac-rhy
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/14.png?raw=true)
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/15.png?raw=true)
  
### Data Governance:
- Built Data Quality Check in AWS Glue Studio for checking the quality of dataset.
- Quality checks applied:
   1. Completeness on Business Name
   2. Uniqueness on License Number
   3. Distinct Count on City
- Output routed to specific Passed folder & Failed folder.
  ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/22.png?raw=true)
  ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/23.png?raw=true)
  ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/24.png?raw=true)
  
### Data Monitoring and Controlling:
- Created a Custom CloudWatch Dashboard for centralized monitoring related to AWS services and resources used for developing the Data Analytical platform: licenses-rental-mcr-rhy
- Added Key Monitoring Widgets to the Dashboard such as the S3 Bucket Size Widget for three S3 buckets: business-raw-rhy, business-trf-rhy, business-cur-rhy which helps in visualizing storage growth trends over time, KMS key usage, Estimated service costs and a CloudTrail Alarm for data size > 500,000 KB.
  ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/25.png?raw=true)

## 4. Tools and Technologies utilised:
  - AWS S3 – Cloud storage for raw, transformed, and curated data
  - AWS Glue DataBrew – Data profiling and cleaning
  - AWS Glue ETL & Crawlers – Data transformation and cataloging
  - AWS Athena – SQL-based analytics on cloud
  - AWS CloudWatch – Monitoring and cost tracking
  - AWS KMS – Encryption and security
  - Diagrams via draw.io

## 5. Key Insights:
1. Identified employment distribution using average employee count.
2. Revealed city-wise rental revenue for better financial planning.
3. Ensured data security, traceability, and cost-efficiency.
4. Enabled scalable analytics infrastructure for public data use.



### Project 2 

# **Project Title: Data Wrangling For Recruitment and Selection Procedure at University Canada West.**

## Project Description:
This project focusesd on wrangling recruitment-related data at University Canada West, integrating datasets like referral lists, faculty list, and recruitment list. Using AWS tools such as EC2, Glue DataBrew, Athena, and S3, the project ensures the data is cleaned, transformed, and query-ready for insightful analysis.

## Objective:
To prepare and unify referral, faculty, and recruitment datasets to enable University Canada West’s HR and academic departments to streamline the hiring pipeline, track sources of hires, and analyze faculty onboarding patterns.

## 1. Dataset:
- Format: CSV
  
  1.**Referral List**
  - Referral ID
  - Referrer Name
  - Referred Candidate Name
  - Referral Source
  - Date Referred
  - Status
  
  2.**Faculty List**
  - Faculty ID
  - Name
  - Department
  - Qualification
  - Date of joining
  - Current Status

  3.**Recruitment List**
  - Candidate ID
  - Name
  - Position Applied
  - Application Date
  - Interview Dates
  - Final Decision
  - Hired Status


## 3. Methodology:
### Data Ingestion:
- Uploaded all datasets CSV to S3 by implementing AWS EC2 services with a remote server.

### Data Cleaning:
- Used AWS Glue DataBrew for:
1. Removing missing or redundant rows
2. Standardizing name and date formats
3. Delete Errors in the data

### Data Transformation:
-Applied Glue jobs to Merge referral and recruitment lists on candidate name, Map faculty qualifications to department needs, Flag inconsistencies in hiring decisions.

### Data Cataloging:
- Cataloged metadata in AWS Glue Data Catalog
- Set column-level metadata
Defined schemas and partitions
- Built Visual ETL Pipeline in Glue
- 
### Data Quering:
- Executed Athena SQL queries to answer:
- How many referrals converted to hires?
- Which departments had the most faculty applications?
- Average time from application to hiring

### Data Security & Lifecycle rules:
- Implemented S3 lifecycle rules for S3 buckets policies
- Restricted access to dataset by using KMS custome key and IAM roles.
  
### Data Monitoring and Controlling:
- Created a Custom CloudWatch Dashboard for centralized monitoring 
- Added Key Monitoring Widgets to the Dashboard such as the S3 Bucket Size Widget for three S3 buckets.
  
## 4. Tools and Technologies utilised:
  - AWS EC2 – Dataset ingestion
AWS Glue & DataBrew – Cleaning and transformation
AWS Glue Data Catalog – Schema and metadata tracking
AWS Athena – SQL-based querying
AWS S3 – Storage with lifecycle rules
IAM – Security and access management
CloudWatch - Data monitoring and controlling.

## 5. Key Insights:
1. 30% of hired faculty were referrals.
2. Science and Business departments received the highest number of applications.
3. Average time-to-hire: 18 days from application to final decision.


## AWS Cloud Foundation Certificate and Badge.

![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/AWS%20Certificate.png?raw=true)
![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/Images/aws-academy-graduate-aws-academy-cloud-foundations.png?raw=true)

   
