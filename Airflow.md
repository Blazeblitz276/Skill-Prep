# Apache Airflow Interview preparation guide

## What is Apache Airflow?

Apache Airflow is a platform to programmatically author, schedule and monitor workflows. Use airflow to author workflows as directed acyclic graphs (DAGs) of tasks. The airflow scheduler executes your tasks on an array of workers while following the specified dependencies. Rich command line utilities make performing complex surgeries on DAGs a snap. The rich user interface makes it easy to visualize pipelines running in production, monitor progress, and troubleshoot issues when needed. When workflows are defined as code, they become more maintainable, versionable, testable, and collaborative.

## What is a DAG?

A Directed Acyclic Graph (DAG) is a collection of all the tasks you want to run, organized in a way that reflects their relationships and dependencies. A DAG’s definition is written in Python files that are placed in Airflow’s DAG_FOLDER. These files can contain the full definition of what the DAG is, and the tasks that it consists of, and what the dependencies are between these tasks.

```python

from airflow import DAG
from airflow.operators.dummy_operator import DummyOperator
from datetime import datetime

dag = DAG('tutorial', description='Simple tutorial DAG',
          schedule_interval='0 12 * * *',
          start_date=datetime(2017, 3, 20), catchup=False)

# t1, t2 and t3 are examples of tasks created by instantiating operators
t1 = DummyOperator(task_id='t1', retries=3, dag=dag)
t2 = DummyOperator(task_id='t2', retries=3, dag=dag)
t3 = DummyOperator(task_id='t3', retries=3, dag=dag)

t1 >> t2
t1 >> t3

etl_dag = DAG(
    dag_id='etl_pipeline',
    default_args= {
        "start_date": datetime(2021, 1, 1)
    }
)
```

- running the task can be done using shell command `airflow run tutorial t1 2017-03-20`

```shell
airflow tasks test <dag_id> <task_id> [execution_date]
```

## General procedure to create a DAG

1. Import the necessary modules

```python
from airflow import DAG
from airflow.operators.dummy_operator import DummyOperator
from datetime import datetime
```

2. Define the default arguments

```python
default_args = {
    'owner': 'airflow',
    'depends_on_past': False,
    'start_date': datetime(2021, 1, 1),
    'email_on_failure': False,
    'email_on_retry': False,
    'retries': 1,
}
```

3. Instantiate the DAG object

```python
dag = DAG(
    'etl_pipeline',
    default_args=default_args,
    description='A simple ETL pipeline',
    schedule_interval='@daily',
)
```
