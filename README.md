
# **Airflow ETL Pipeline – File Based Data Processing**
# 📋 **Project Overview**

This project implements an **ETL (Extract, Transform, Load) pipeline**
using **Apache Airflow** to process customer data from CSV files. 
The pipeline reads raw data, performs cleaning and transformations, and saves the processed data into a new CSV file.

# 📌 **What is ETL?**

| Step      | Description                          |
| --------- | ------------------------------------ |
| Extract   | Read data from source file           |
| Transform | Clean, validate, and enrich data     |
| Load      | Save transformed data to destination |

# 🛠️ **Technologies Used**

| Technology              | Purpose                             |
| ----------------------- | ----------------------------------- |
| Apache Airflow 2.9.3    | Workflow orchestration & scheduling |
| Docker & Docker Compose | Containerized environment           |
| Python 3.8+             | ETL logic implementation            |
| Pandas                  | Data manipulation & transformation  |
| PostgreSQL              | Airflow metadata storage            |
| Git & GitHub            | Version control & collaboration     |

# 📁 **Project Structure**

* **dags/** → Contains Airflow DAG files
* **data/** → Input and output data files
* **logs/** → Airflow logs
* **scripts/** → Python ETL scripts
* **.env** → Environment variables
* **docker-compose.yaml** → Container setup

# 🔄 **ETL Process Flow**

**Input CSV → Extract → Transform → Load → Output CSV**

# 📥 **Extract Task**

* Reads `customers.csv` from `/data/input/`
* Validates file existence
* Loads data into Pandas DataFrame

# 🔄 **Transform Task**

The following transformations are applied:

| Operation     | Description                              |
| ------------- | ---------------------------------------- |
| Missing Email | Fills with `unknown@email.com`           |
| Missing Age   | Fills with median age value              |
| Invalid Email | Marks as `invalid@email.com`             |
| City Names    | Capitalizes and removes whitespace       |
| Age Segment   | Creates categories: Young, Adult, Senior |
| Active Status | Marks customers with `spent_amount > 0`  |
| Timestamp     | Adds transformation timestamp            |

# 📤 **Load Task**

* Saves transformed data to `/data/output/`
* Creates timestamped filename:
  `transformed_customers_YYYYMMDD_HHMMSS.csv`
* Generates summary report

# 📊 **Sample Data**

## **Input Data (customers.csv)**

| customer_id | name       | email                                   | age | city        | spent_amount |
| ----------- | ---------- | --------------------------------------- | --- | ----------- | ------------ |
| 1           | John Doe   | [john@email.com](mailto:john@email.com) | 35  | New York    | 250.50       |
| 2           | Jane Smith | [jane@email.com](mailto:jane@email.com) | 28  | Los Angeles | 180.00       |
| 3           | Bob Wilson | invalid-email                           | 42  | Chicago     | 0            |

---

### **Output Data (After Transformation)**

| name       | email                                         | age | city        | segment | is_active | transformed_at      |
| ---------- | --------------------------------------------- | --- | ----------- | ------- | --------- | ------------------- |
| John Doe   | [john@email.com](mailto:john@email.com)       | 35  | New York    | Adult   | True      | 2026-04-27 8:30:18
| Jane Smith | [unknown@email.com](mailto:unknown@email.com) | 28  | Los Angeles | Young   | True      | 2026-04-27 8:30:18 |
| Bob Wilson | [invalid@email.com](mailto:invalid@email.com) | 42  | Chicago     | Adult   | False     | 2026-04-27 8:30:18|

# ⚙️ **Setup Instructions**

## **1. Clone the Repository**

https://github.com/Moomnaatiq808/airflow-file-etl.git

## **2. Navigate to Project Folder**

cd airflow-file-etl

## **3. Run Docker Containers**
docker-compose up -d

## **4. Open Airflow UI**
http://localhost:8081

## 🎯 **Conclusion**

This project demonstrates a complete **file-based ETL pipeline** using Apache Airflow.
It automates data processing, ensures data quality, and provides structured output for further analysis.


## 📌 **Project Description**

ETL Pipeline using Apache Airflow with Docker
