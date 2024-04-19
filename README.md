# ELT-Docker-Airflow

This repository houses an ELT pipeline encapsulated within Docker containers. It is engineered to extract data from a source Postgres database, transfer it seamlessly to a destination Postgres database, and subsequently execute transformations using a DBT model within the destination database. Additionally, the repository includes integration capabilities for scheduling CRON jobs, and the entire pipeline is automated through Airflow.

### Repository Structure
1. <b>airflow</b>: This folder contains the configuration for Airflow.
   * <b>airflow/dags/elt_dag.py</b>: python script for the Airflow dags
2. <b>custom_postgres</b>: This folder contains the configuration for the DBT model.
   * <b>custom_postgres/models/example/*.sql</b>: SQL scripts with references to the tables in the destination database
   * <b>custom_postgres/models/example/schema.yaml</b>: yaml file with the schema for the tables in the destination database
   * <b>custom_postgres/models/example/sources.yaml</b>: yaml file for the destination database
3. <b>elt_script</b>: This folder contains the resources for the ELT activity.
   * <b>elt_script/Dockerfile</b>: This Dockerfile sets up a Python environment and installs the PostgreSQL client. It also copies the ELT script into the container and sets it as the default command along with the configuration for the CRON job.
   * <b>elt_script/elt_script.py</b>: This Python script performs the ELT process. It waits for the source PostgreSQL database to become available, then dumps its data to an SQL file and loads this data into the destination PostgreSQL database.
4. <b>source_db_init</b>: This folder houses the SQL script that initializes the source database with sample data. It creates tables for users, films, film categories, actors, and film actors, and inserts sample data into these tables.
5. <b>Dockerfile</b>: This file sets up the Airflow environment.
6. <b>docker-compose.yaml</b>: Using this file, the following Docker containers are spun up:
   * Source Postgres database with example data
   * Destination Postgres database
   * Postgres database for Airflow
   * Airflow service
   * Webserver for Airflow
   * Scheduler for Airflow  
