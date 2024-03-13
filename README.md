
# Build a Simple ETL with Airflow, PostgreSQL and Docker

# Goal
Try to build a simple ETL with Airflow, PostgreSQL and Docker

# Implementation Process
I followed this [Medium article](https://intuitivedataguide.medium.com/building-a-simple-etl-with-airflow-postgresql-and-docker-a2b1a2b202ec).
The github repo can be found at [here](https://github.com/sevkw/airflow-etl/tree/master)

# Issue
Airflow DAG recalls_etl_v1.py and PostgreSQL Database was created, however, the DAG recalls_etl_v1 failed due to ERROR - Failed to execute job 10 for task get_raw_data (Unterminated string starting at: line 1 column 3244243 (char 3244242); 2199).
