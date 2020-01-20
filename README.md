# airflowProject
A sample for the airflow project structure

1. A project is normally something completely separate or unique. Perhaps DAGs to process files that we receive from a certain client which will be completely unrelated to everything else (almost certainly a separate database schema)
2. We can have the operators, hooks, and some helper scripts (delete all Airflow data for a certain DAG, etc.) in a common folder.
3. We can have a single git repository for the entire Airflow folder, but now we have a separate git per project (makes it more organized and easier to grant permissions on Gitlab since projects are so unrelated). This means that each project folder also as a .git and .gitignore, etc as well
4. We tend to save the raw data and then 'rest' a modified copy of the data which is exactly what gets copied into the database. We have to heavily modify some of the raw data due to different formats from different clients (Excel, web scraping, HTML email scraping, flat files, queries from SalesForce or other database sources...)


Example tree:

├───dags
│   ├───common
│   │   ├───hooks
│   │   │       pysftp_hook.py
│   │   │
│   │   ├───operators
│   │   │       docker_sftp.py
│   │   │       postgres_templated_operator.py
│   │   │
│   │   └───scripts
│   │           delete.py
│   │
│   ├───project_1
│   │   │   dag_1.py
│   │   │   dag_2.py
│   │   │
│   │   └───sql
│   │           dim.sql
│   │           fact.sql
│   │           select.sql
│   │           update.sql
│   │           view.sql
│   │
│   └───project_2
│       │   dag_1.py
│       │   dag_2.py
│       │
│       └───sql
│               dim.sql
│               fact.sql
│               select.sql
│               update.sql
│               view.sql
│
└───data
    ├───project_1
    │   ├───modified
    │   │       file_20180101.csv
    │   │       file_20180102.csv
    │   │
    │   └───raw
    │           file_20180101.csv
    │           file_20180102.csv
    │
    └───project_2
        ├───modified
        │       file_20180101.csv
        │       file_20180102.csv
        │
        └───raw
                file_20180101.csv
                file_20180102.csv
