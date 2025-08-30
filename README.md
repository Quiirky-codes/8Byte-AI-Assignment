# Stock Data Pipeline with Airflow & Postgres

Amith M Jain developed this project as part of an assignment for 8byte.ai.
It sets up an end-to-end pipeline to fetch stock market data from Alpha Vantage API and store it in a PostgreSQL database using Apache Airflow.

# Features

* Fetches stock market data from Alpha Vantage API

* Stores data in a Postgres database

* Orchestrated using Apache Airflow

* Dockerized for easy setup

# Prerequisites

* Docker

* Docker Compose

* An Alpha Vantage API key

# Project Structure

```
stock-pipeline-airflow/
│── docker-compose.yml         
│── .env.example               
│── dags/
│   └── stock_dag.py           
│── scripts/
│   └── fetch_and_store.py     
│── sql/
│   └── init.sql               
```

# Setup Instructions
## 1. Clone the repository

```
git clone "https://github.com/Quiirky-codes/8Byte-AI-Assignment.git"
cd 8Byte-AI-Amith
```

## 2. Configure environment variables

* Copy .env.example → .env and fill in your details:

## Required: Get your API key from Alpha Vantage

```
ALPHAVANTAGE_API_KEY=your_api_key
```

## 3. Start the services

```
docker-compose up -d --build
```

* This will spin up:

_Postgres on port 5432_

* Airflow Web UI on port 8080 → http://localhost:8080

## Login with:

Username: admin

Password: admin

<img width="1808" height="1062" alt="image" src="https://github.com/user-attachments/assets/4fb5bd1d-6875-4a4a-89cc-6c86f3796b47" />


# Running the Pipeline

## 1. Start Airflow Scheduler manually

* By default, Airflow is running, but you may need to ensure the scheduler is active.
Run this inside the Airflow container:

```
docker exec -it airflow bash
airflow scheduler
```

## 2. Trigger the DAG

* Open Airflow UI → http://localhost:8080

* Enable and trigger stock_dag

<img width="2920" height="1460" alt="image" src="https://github.com/user-attachments/assets/42fb757f-1975-4567-a99a-e7e2953a92a9" />


# Checking Data in Postgres

* To connect to the database and verify inserted stock data:

```
docker exec -it postgres psql -U amithmjain -d stockdb
```

Inside psql:

```
\dt;                         
SELECT * FROM stock_prices;  
```

<img width="1988" height="426" alt="image" src="https://github.com/user-attachments/assets/c304c253-36df-4204-8a9f-4e18dc69ddc4" />


# ✅ Notes

The pipeline runs daily (not hourly).

If DAG tasks fail, check logs in the Airflow UI.

Ensure your Alpha Vantage API key is valid (free tier has request limits).
