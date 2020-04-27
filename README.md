# Data Modeling with Postgres

## Create a Postgres database with tables designed to optimize queries on song play analysis

### Introduction

A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

As a data engineer, I've created a Postgres database with tables designed to optimize queries on song play analysis. My role is to create a database schema and ETL pipeline for this analysis, test the database I created and ETL pipeline by running queries given to me by the analytics team from Sparkify and compare my results with their expected results.

### Description

In this project I will apply data modeling concepts with Postgres and build an ETL pipeline using Python. I will define fact and dimension tables for a star schema and write an ETL pipeline that transfers data from files in two local directories into these tables in Postgres using Python and SQL.

### Files

1. `test.ipynb` displays the first few rows of each table to check the database.
2. `create_tables.py` drops and creates your tables. You run this file to reset your tables before each time you run your ETL scripts.
3. `etl.ipynb` reads and processes a single file from `song_data` and `log_data` and loads the data into your tables. This notebook contains detailed instructions on the ETL process for each of the tables.
4. `etl.py` reads and processes files from `song_data` and `log_data` and loads them into your tables.
5. `sql_queries.py` contains all the SQL queries, and is imported into the last three files above.

### Schema Design for the Song Play Analysis
Using the song and log datasets, I've created a star schema optimized for queries on song play analysis. This includes the following tables:

#### Fact Table
1. **songplays** - records in log data associated with song plays i.e. records with page **NextSong**
* *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

#### Dimension Tables
2. **users** - users in the app
* *user_id, first_name, last_name, gender, level
3. **songs** - songs in the music database
* *song_id, title, artist_id, year, duration
4. **artists** - artists in the music database
* *artist_id, name, location, latitude, longitude
5. **time** - timestamps of records in **songplays** broken down into the specific unit
* *start_time, hour, day, week, month, year, weekday

### ETL - Song Data
I will perform ETL on the files in the *song_data* directory to create two dimensional tables: `songs` and `artists`.

1. The first part of this process is extracting the data from the JSON files by using the designated columns in the schema.
2. Then I will insert the extracted data into their respective tables using SQL queries.

### ETL - Log Data
For the remaining dimension tables, `time` and `users`, I will perform ETL on the files in the *log_data* directory.

1. For the `time` table, I will parse the data from the *ts* column in the log files by using python's datetime functions and then transfer it into the appropriate columns.
2. Then, for the `users` table I will simply extract the columns specified in the schema and insert it into its table. 
3. Lastly, I will create the remaining fact table, *songplays*, by executing a query on the *songs* and *artists* tables and pulling data from the log files.


### Use
#### Sample Test Run
1. Run `create_tables.py` to create tables from all the queries located in `sql_queries.py`.
2. Run `etl.ipynb` to insert a single file from song_data and log_data into our tables.
3. Run `test.ipynb` to confirm your records were successfully inserted into each table.

#### Official Prod Run
1. Run `create_tables.py` to reset the tables. This will drop all the tables and create new ones for a fresh start.
4. Run `etl.py` to read and process all files from song_data and log_data and load them into our tables.
5. Run `test.ipynb` to confirm your records were successfully inserted into each table.
 

NOTE: You will not be able to run test.ipynb, etl.ipynb, or etl.py until you have run create_tables.py at least once to create the sparkifydb database, which these other files connect to.

