
### **🛠 Project Overview**

Title: lab-data-pipelines-airflow

Description: 
This repository provides a hands-on introduction to Apache Airflow, a platform used to programmatically author, schedule, and monitor workflows. You will learn how to define Directed Acyclic Graphs (DAGs) to automate data pipelines. The lab covers the use of various operators (Bash, Python, and Email) to create a sequence of tasks that execute based on dependencies and schedules.

<br>

### **🛠 Prerequisites**

Before you begin, ensure you have the following installed:
1. Python 3.8+: Airflow is a Python-based framework.
2. Apache Airflow Instance: A local installation or a managed service (like Astronomer or Managed Workflows for Apache Airflow).
3. Linux/macOS Environment: Airflow is designed for POSIX-compliant operating systems (Windows users should use WSL2).
4. SMTP Server Access: Required if you wish to actually send emails using the EmailOperator.

<br>

### 🛠 **Directed Acyclic Graphs (DAG)**

#### DAG (Directed Acyclic Graphs) Structure and Operators:
- Imports
- DAG Arguments
- DAG Definition
- Task Definitions
- Task Pipeline

<br>

### 🛠 **Sample Code**

import the libraries
```Bash
from datetime import timedelta
```

The DAG object; we'll need this to instantiate a DAG
```Bash
from airflow.models import DAG
```

Operators; you need this to write tasks!
```Bash
from airflow.operators.bash_operator import BashOperator
from airflow.operators.python import PythonOperator
from airflow.operators.email import EmailOperator
```

defining DAG arguments
```Bash
default_args = {
    'owner': 'Your name',
    'start_date': days_ago(0),
    'email': ['youemail@somemail.com'],
    'retries': 1,
    'retry_delay': timedelta(minutes=5),
}
```

define the DAG
```Bash
dag = DAG(
    dag_id='unique_id_for_DAG',
    default_args=default_args,
    description='A simple description of what the DAG does',
    schedule_interval=timedelta(days=1),
)
```


** define the tasks with BashOperator or PythonOperator **

define a task with BashOperator
```Bash
task1 = BashOperator(
    task_id='unique_task_id',
    bash_command='<some bashcommand>',
    dag=dag,
)
```

define a task with PythonOperator
```Bash
task2 = PythonOperator(
    task_id='bash_task',
    python_callable=<the python function to be called>,
    dag=dag,
)
```

define a task with EmailOperator
```Bash
task3 = EmailOperator(
    task_id='mail_task',
    to='recipient@example.com',
    subject='Airflow Email Operator example',
    html_content='<p>This is a test email sent from Airflow.</p>',
    dag=dag,
)
```

task pipeline
```Bash
task1 >> task2 >> task3
```

<br>

### 🛠 **How to Practice**

Run the command below in the terminal to list all the existing DAGs.
```Bash
airflow dags list
```

Run the command below in the terminal to list all tasks in the DAG named example_bash_operator.
```Bash
airflow tasks list example_bash_operator
```

Run a command to list all tasks for the DAG named tutorial.
```Bash
airflow tasks list tutorial
```

Run the command below in the terminal to unpause a DAG named tutorial.
```Bash
airflow dags unpause tutorial
```

Run the command to pause the DAG.
```Bash
airflow dags pause tutorial
```


<br>

### 🛠 **Practice exercises**

<br>

1. coursework first_dag
    - Directory: lab_first_dag
    - Open my_first_dag_bash_operator.py. Complete the task using the BashOperator to run a simple echo command.
    - Open my_first_dag_python_operator.py. Define a Python function and call it using the PythonOperator.
    - Open practice_my_first_dag.txt, Practice the workflow

<br>

2. coursework dummy_dag
    - Directory: lab_dummy_dag
    - Open dummy_dag.py. Complete the task using to run a simple echo command.
    - Open practice_dummy_dag.txt, Practice the workflow

