# Airport Baggage Screening Report | Apache Airflow

## Project Overview

This project implements an automated Airport Baggage Screening workflow using Apache Airflow.

The workflow processes baggage records from a CSV file, identifies bags requiring manual review based on screening status or weight, calculates the total baggage weight, and generates a summary report.

## Business Requirement

An airport operations team needs to:
- Process baggage records.
- Identify bags requiring manual review.
- Calculate the total weight of all baggage.
- Generate a screening summary report.

## Technologies Used

- Python
- Apache Airflow 3.4.0
- Docker
- CSV

## Airflow Concepts Implemented

- **DAG:** Defines the baggage screening workflow.
- **PythonOperator:** Executes Python functions as Airflow tasks.
- **XCom:** Transfers data between tasks.
- **Task Dependencies:** Controls the execution order.
- **Parallel Execution:** Runs baggage review identification and weight calculation independently.

## Workflow Architecture

```text
load_baggage
      |
      |
      +-----------------------+
      |                       |
      v                       v
identify_review_bags    calculate_total_weight
      |                       |
      +-----------+-----------+
                  |
                  v
            generate_report
```

## Task Description

| Task | Description |
|---|---|
| load_baggage | Reads six baggage records from the CSV file. |
| identify_review_bags | Identifies bags with screening status Review or weight above 23 kg. |
| calculate_total_weight | Calculates the total weight of all baggage. |
| generate_report | Collects results using XCom and prints the final report. |

## Input Dataset

File: `airport_baggage.csv`

The dataset contains six baggage records with the following columns:

- `bag_id`
- `flight_no`
- `weight_kg`
- `screening_status`

## Screening Logic

A baggage item requires manual review if:

- Its screening status is `Review`, OR
- Its weight is greater than 23 kg.

## Expected Results

- Total baggage records: 6
- Bags requiring review: BG102, BG103, BG105
- Total baggage weight: 119 kg

## DAG Configuration

- **DAG ID:** `airport_baggage_pipeline`
- **Schedule:** None (manual trigger)
- **Catchup:** False
- **Execution Environment:** Killercoda Docker environment

## Execution

1. Start the existing Airflow Docker environment.
2. Place the DAG and CSV files in the Airflow DAGs directory.
3. Validate the Python file.
4. Open the Airflow UI on port 8080.
5. Trigger `airport_baggage_pipeline` manually.
6. Inspect the Graph view and task logs.

## Screenshots

Project execution screenshots are available in the `screenshots` folder.

## Key Learning Outcomes

- Building workflow pipelines using Apache Airflow.
- Implementing PythonOperator tasks.
- Passing data between tasks using XCom.
- Designing parallel task execution.
- Monitoring DAG execution through Graph and Grid views.
- Generating reports through Airflow task logs.

---

**Project:** Airport Baggage Screening Report  
**Category:** Data Engineering | Workflow Orchestration
