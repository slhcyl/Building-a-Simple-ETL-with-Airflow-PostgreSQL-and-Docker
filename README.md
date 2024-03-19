
# Build a Simple ETL with Airflow, PostgreSQL and Docker

# Goal
Try to build a simple ETL with Airflow, PostgreSQL and Docker

# Implementation Process
I followed this [Medium article](https://intuitivedataguide.medium.com/building-a-simple-etl-with-airflow-postgresql-and-docker-a2b1a2b202ec).
The github repo can be found at [here](https://github.com/sevkw/airflow-etl/tree/master)

# Issue
Airflow DAG recalls_etl_v1.py and PostgreSQL Database was created, however, the DAG recalls_etl_v1 failed due to ERROR - Failed to execute job 10 for task get_raw_data (Unterminated string starting at: line 1 column 3244243 (char 3244242); 2199).
I conntaced the original owner of this process and got the reply from him. By running the following code, I was unable to get the 200 records. It indicates the original API was corrupted and wasn't fixed by the IT team.
```
import requests

raw_url = 'https://recalls-rappels.canada.ca/sites/default/files/opendata-donneesouvertes/HCRSAMOpenData.json'

def get_recall_data(url):
    response = requests.get(url)
    response_data = response.json()
    print(response)

get_recall_data(raw_url)
```
# My Implementation:
## 1. Change json API to a sample json file.
Due to json API was broken, I extracted a sample json file from the website and saved it under airflow/dags.

## 2. Modify the data path:
```
# data path to save raw data and cleaned data
raw_data_path = '/opt/airflow/recalls_raw.csv'
cleaned_data_path = '/opt/airflow/recalls_cleaned.csv'
file = '/opt/airflow/dags/sample.json'
```
The original code is shown below. But I kept getting the error message 'Cannot save file into a non-existent directory: '/opt/***/data'; 2801'. 
```
raw_data_path = '/opt/airflow/data/raw/recalls_raw.csv'
cleaned_data_path = '/opt/airflow/data/cleaned/recalls_cleaned.csv'
```
I tried to configured it at docker-compose.yaml file as shown below, but it didn't solve the problem.
```
 volumes:
    - ${AIRFLOW_PROJ_DIR:-.}/dags:/opt/airflow/dags
    - ${AIRFLOW_PROJ_DIR:-.}/logs:/opt/airflow/logs
    - ${AIRFLOW_PROJ_DIR:-.}/config:/opt/airflow/config
    - ${AIRFLOW_PROJ_DIR:-.}/plugins:/opt/airflow/plugins
    - ${AIRFLOW_PROJ_DIR:-.}/data:/opt/airflow/data
```
Instead, I simply removed '/data/raw' and '/data/cleaned' from the path and airflow DAG ran successfully without errors. I was able to see the end results from recalls_db.data.recalls in DBeaver.
If someone ran into similiar issues, feel free to chat here. 
