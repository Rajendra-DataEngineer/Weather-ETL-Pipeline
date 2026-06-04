# 🌦️ Weather ETL Pipeline — API → Azure → Databricks

## 📌 Project Overview
An end-to-end data pipeline that extracts live weather data from OpenWeatherMap API 
for 9 major UK cities, stores raw JSON in Azure Blob Storage, transforms it using 
PySpark on Databricks, and saves analytics as Delta Lake tables.

---

## 🏗️ Architecture
OpenWeatherMap API → Python Extract → Azure Blob Storage → Databricks PySpark → Delta Table

---

## ⚙️ Tech Stack
- Python (requests, azure-storage-blob)
- OpenWeatherMap API
- Azure Blob Storage
- Apache Spark / PySpark
- Databricks (Serverless)
- Delta Lake

---

## 🔄 Pipeline Phases

### 1️⃣ Extract (fetch_weather.py)
- Calls OpenWeatherMap API for 9 UK cities
- Birmingham, Bristol, Edinburgh, Glasgow, Leeds, Liverpool, London, Manchester, Sheffield
- Saves raw JSON files locally and uploads to Azure Blob Storage (`weather-raw` container)

### 2️⃣ Transform (Databricks Notebook)
- Reads raw JSON files from Azure Blob Storage
- Extracts key fields: city, temperature, humidity, wind speed, weather description
- Converts Unix timestamp to readable datetime
- Rounds numeric values for consistency
- Adds load timestamp column

### 3️⃣ Load
- Saves transformed data as Delta Table: `gold_weather_uk`
- Queryable with Spark SQL

---

## 📊 Sample Output

| City | Temp (°C) | Weather | Wind Speed |
|------|-----------|---------|------------|
| Bristol | 24.1 | Few clouds | 0.9 |
| Birmingham | 22.5 | Scattered clouds | 0.5 |
| Sheffield | 20.0 | Broken clouds | 0.9 |
| London | 17.6 | Overcast clouds | 4.0 |
| Edinburgh | 14.3 | Overcast clouds | 1.3 |

---

## 🚀 How to Run

### Extract Phase
1. Add your credentials to `.env`:
WEATHER_API_KEY=your_openweathermap_api_key
AZURE_CONNECTION_STRING=your_azure_connection_string
AZURE_CONTAINER_NAME=weather-raw
2. Run:
python extract/fetch_weather.py

### Transform Phase
1. Import `weather-transform-pipeline.ipynb` into Databricks
2. Update `CONN_STR` with your Azure connection string
3. Run all cells

---

## 📁 Project Structure
weather-etl-pipeline/
├── extract/
│   └── fetch_weather.py        # API extraction script
├── .gitignore
├── requirements.txt
├── weather-transform-pipeline.ipynb  # Databricks notebook
└── README.md














Made by Rajendra K
Aspiring Azure Data Engineer | Open to UK & Europe Opportunities







