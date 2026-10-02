-- =====================================================
# 9. README - NOAA Weather ETL Pipeline
-- =====================================================


-- ==================
#  Project Overview
-- ==================

This project implements an ETL pipeline for processing historical NOAA 
Weather data from 2015 to 2020.

The pipeline extracts data from multiple CSV files, cleans and transforms the data,
Performs data quality checks, and loads the processed data into PostgreSQL.

Logging and error handling are also implemented to monitor pipeline execution
And capture failures. 

-- ==================
#  Objectives
-- ==================

A weather analytics company receives weather data from several CSV files.

The company needs an ETL pipeline to validate incoming files, extract, clean
And transform the data, check data quality , and load the processed data
Into a PostgreSQL database for analysis.

-- ==================
#  Dataset
-- ==================


Dataset: GHCN Daily Weather Data by City (2015–2020)

Source: Kaggle  
[GHCN Daily Weather Data by City (2015–2020)](https://www.kaggle.com/datasets/abhijitk1/weather-data-by-city-20152020)

Period: 2015–2020

Number of source files: 6 CSV files

The six yearly CSV files are combined into one DataFrame during the extraction process.

-- ====================
#  Tools & Technologies
-- ====================

- Python
- Pandas
- PostgreSQL
- SQLAlchemy
- psycopg2
- Jupyter Notebook
- Python logging
- Markdown
- GitHub

-- ====================
#  Project Structure
-- ====================

ETL Pipeline


The pipeline follows these steps:

CSV Files
    ↓
Extract
    ↓
Clean
    ↓
Transform
    ↓
Data Quality Check
    ↓
Load into PostgreSQL


-- ====================
#  ETL Pipeline Workflow
-- ====================

### Step 1. Extract Data
The pipeline reads six CSV files containing weather data from 2015 to 2020 and 
Combines them into one DataFrame.

### Step 2. Clean Data
Duplicate records are removed, and rows with missing values in the required columns
('Date' and 'ID' in this project) are dropped.

### Step 3. Transform and Standardize Data
Dates are converted to a standard datetime format, and temperature measurements
(TAVG, TMAX, and TMIN) are divided by 10 to convert NOAA temperature values 
To degree Celsius (°C).

### Step 4. Data Quality Checks
Before loading the data into PostgreSQL, the pipeline checks for duplicate records and missing values in the required columns.
If duplicate records or missing required values are detected, the pipeline raises a ValueError and stops. Otherwise, the data passes the quality check and is loaded into PostgreSQL.

### Step 5: Load Data
After passing the quality checks, the transformed data is loaded into 
`weather_data` table in PostgreSQL using SQLAlchemy.

## step 6. Logging and Error Handling
Python's logging module is used to record the execution of the ETL pipeline.

The pipeline logs:

- Pipeline start
- Number of extracted records
- Number of cleaned records
- Number of transformed records
- Data quality validation
- Successful PostgreSQL Load
- Pipeline completion
- Pipeline failures

Log file:

logs/pipeline.log

The pipeline uses try/except error handling so that failures are captured and
recorded  in the log file.

-- ====================
#  Data Quality Report
-- ====================

The final data quality check passed successfully:

- Duplicate records: 0
- Missing values in required columns (`Date` and `ID`): 0
- Final records: 11,379,747
- Status: PASSED

For detailed validation results , see 'data_quality_report.md`.

-- ====================
#  Scaling the Pipeline
-- ====================

**Question:** If this dataset grew from 1 GB to 10 TB, what would you change?

**Answer:**  
To improve scalability and performance, I would:


- Use Parquet instead of CSV to reduce storage and improve query performance.
- Partition the data, for example by year, month, or station, so pipeline 
Only reads the required data.
- Process new data incrementally instead of reprocessing the entire dataset
On every run.
- Use Apache Spark/PySpark instead of pandas for distributed processing of large datasets.
- Compress the files to reduce storage costs and I/O.
- Add appropriate indexes to frequently queried columns to improve query performance.
- Cache frequently reused intermediate data to avoid repeated processing
And improve performance.
_ Improve monitoring and logging by tracking pipeline status(success or failure) ,processing time,
Record counts , and data quality errors.


-- ====================
#  Conclusion
-- ====================

This project demonstrates an end-to-end ETL pipeline for processing 
NOAA weather data.

The pipeline extracts, cleans, transforms, performs data quality checks ,and loads 
Weather data into PostgreSQL while using Logging and error handling 
To improve reliability.










