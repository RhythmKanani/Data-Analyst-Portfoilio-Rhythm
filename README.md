### Project 1 

# **Data Aanalytical Platform For City Of Vancouver - Rental Business Licenses.**

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
- ![Diagram showing the Data ingestion of rental list to S3 bucket.]()
- ![Ingestion Successful of rental list dataset to S3 Bucket from.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/image.png?raw=true)
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
- [Diagram showing the Data ingestion of rental list to S3 bucket.](https://github.com/RhythmKanani/Data-Analyst-Portfoilio-Rhythm/blob/main/image.png?raw=true)
   
