# SUBMITTED-ds2002-midterm-project
Data Systems 2002 Midterm Project – Rentals-based Data Mart

This project constructs a simplified data warehouse from the `sakila` MySQL database using a dimensional star schema. It demonstrates ETL processing from three distinct data sources into a central fact table (`fact_rentals`) and associated dimensions.

Project Overview

Fact Table: 'fact_rentals'
Dimensions:
'dim_film" (JSON)
'dim_language' (MySQL)
'dim_store' (MongoDB)
'dim_date'

ETL Process Summary

Data Sources: 
-MySQL ('sakila'): raw tables such as 'rental', 'language', and 'film'
-JSON File ('film_data.json`
-MongoDB (`store_data.json`)

Transformations:
-All of the dimension tables were eliminated and were assigned to surrogate keys (`*_key`)
-The fact table was joined using natural keys and supplemented with foreign keys to dimensions
- Date keys were resolved using the `dim_date` table based on actual rental dates

Fact Table Fields:
- `fact_rental_key` (PK)
- `store_key`, `film_key`, `language_key`, `rental_date_key`
- Coming from `rental`, `inventory`, and `film` tables

Code Structure
- `load_data_from_mysql()` / `write_data_to_mysql()`: handles SQL extraction and insertion
- `connect_to_mongo()` / `load_collection_as_df()`: connects to MongoDB Atlas and loads collections
- JSON data is directly read using Pandas and transformed into dimension tables
- All transformations are handled using Pandas DataFrames

Deployment Strategy
1. Local MySQL is used to host the source (`sakila`) and warehouse (`sakila_dw`) databases
   Use `sakila-schema.sql`, `sakila-data.sql`, and `Create_Dim_Date.sql` to set up
2. MongoDB is used to host the `store` collection (pre-uploaded
  Credentials configured in the notebook
3. Jupyter Notebook (`Submitted-DS 2002 Midterm Project.ipynb`) contains the full ETL pipeline
4. Supporting SQL scripts like `Create_Dim_Date.sql` and `sakila-schema.sql` are used to set up required schema

Summary
This project demonstrates building a multi-source schema warehouse using Python, SQL, MongoDB, and Pandas — reproducible via Jupyter Notebook
