
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
