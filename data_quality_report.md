
NOAA Weather ETL – Data Quality Report

1. Dataset Overview

This report summarizes the data quality checks during the NOAA Wether ETL pipeline.

The dataset contains historical weather data collected from six CSV files covering the years 2015-2020.

The ETL pipeline extracts the raw data , removes duplicate records, handling missing values in required columns, standardizes dates and temperature units, validates data quality before loading the processed data into PostgreSQL.


| Metric          | Result            |
| --------------- | ----------------- |
| Dataset         | NOAA Weather Data |
| Period          | 2015–2020         |
| Source files    | 6 CSV files       |
| Initial records | 11,379,747        |
| Destination     | PostgreSQL        |


2. Duplicate Records

Duplicate records were checked before and after duplicate removal process.

The pipeline uses Pandas duplicated().sum() to count duplicate rows and drop_duplicates() to remove them.


| Metric                     | Result |
| -------------------------- | ------ |
| Duplicates before cleaning |      0 |
| Duplicates after cleaning  |      0 |


Result: No duplicate records were found before or after cleaning.


3. Missing Values

Missing values were examined before and after the cleaning process.

Date and ID are required columns. Missing values were checked in these required columns.

The pipeline uses Pandas isnull().sum() to check missing values and dropna() to remove rows with missing values, so rows with missing Date or ID values were removed using dropna().

Missing values in other columns were kept.


| Metric                              | Result |
| ----------------------------------- | ------ |
| Missing Date values before cleaning |      0 |
| Missing ID values before cleaning   |      0 |
| Missing Date values after cleaning  |      0 |
| Missing ID values after cleaning    |      0 |


Result: There were no missing values in the required columns, Date and ID.


4. Data Transformation and Standardization

The Date column and temperature values were standardized.

The pipeline uses Pandas pd.to_datetime() to convert the Date column to datetime format.

The pipeline uses Pandas division by 10(/ 10) to convert TAVG, TMAX, and TMIN temperature values to degrees celsius.


Result: This transformed and standardized data is ready for the data quality check.


5. Data Quality Check

After cleaning and transformation , the pipeline checks the data quality before loading the data into PostgreSQL.

The pipeline uses duplicated().sum() to check duplicate records and isnull().sum().sum() to check missing values in the required Date and ID columns.


| Metric                     | Result |
|----------------------------|--------|
| Duplicate records          | 0      |
| Missing Date values        | 0      |
| Missing ID values          | 0      |
| Data quality check         | PASSED |


6. Load Data

After the quality check passed , the transformed data was loaded into PostgreSQL.

The pipeline uses SQLAlchemy create_engine() to connect to connect to PostgreSQL and to_sql() to load the data into the weather_date table.


Result: Data loaded successfully!


6. Build Complete ETL Pipeline 

The run_pipeline() function combines all ETL steps:

Extract → Clean → Transform → Data Quality Check → Load


Result: ETL pipeline completed successfully!


7. Logging and Error Handling

The pipeline uses Python logging to record the ETL steps.

The log file records the Extract, Clean, Transform, Data Quality, and Load steps.

Error handling is used to catch and record errors during the pipeline.

Result: Logging and error handling were added successfully.


8. Final Dataset

| Metric                   | Result                 |
| ------------------------ | ---------------------- |
| Initial records          | 11,379,747             |
| Final records            | 11,379,747             |
| Removed records          | 0                      |
| Final data quality check | PASSED                 |


9. Conclusion

The NOAA Weather ETL pipeline successfully processed weather data from 2015 to 2020.

The data was cleaned ,transformed, checked ,and loaded into PostgreSQL.

The pipeline also uses logging and error handling to record the process and errors.








