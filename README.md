# ELT Pipeline with Docker, Dbt, and Airflow

This project implements an ELT (Extract, Load, Transform) pipeline using Docker, Dbt (Data build tool), and Airflow. The pipeline facilitates data extraction, transformation, and loading processes efficiently.

## Prerequisites

Before running the project, ensure you have the following installed:

- [Dbt Core](https://docs.getdbt.com/docs/core/pip-install?utm_term=&utm_campaign=q3-2024_us-evergreen-prospecting_cv&utm_source=adwords&utm_medium=ppc&hsa_acc=8253637521&hsa_cam=20455348559&hsa_grp=&hsa_ad=&hsa_src=x&hsa_tgt=&hsa_kw=&hsa_mt=&hsa_net=adwords&hsa_ver=3&gad_source=1&gclid=Cj0KCQiAxOauBhCaARIsAEbUSQQ8wodICW6wXNrBW5XOqCKXldLUOtIVfDQ3lP3xAzI-XT4-VnUG4-QaAoKWEALw_wcB)
- [Docker](https://www.docker.com/)

## Setup

1. **Clone the Repository:**


2. **Dbt Configuration:**

- After downloading Dbt Core, navigate to the root folder of the project.
- Locate the `.dbt` directory and find the `profiles.yml` file.
- Edit the `profiles.yml` file by adding the following contents:

  ```yaml
  custom_postgres:
    outputs:
      dev:
        dbname: destination_db
        host: host.docker.internal
        pass: postgres
        port: 5434
        schema: public
        threads: 1
        type: postgres
        user: postgres
    target: dev
  ```

3. **Initialize Apache Airflow:**

- Run the following command from the root directory of the cloned repository:

  ```
  docker compose up init-airflow -d
  ```

4. **Start Services:**

- Once Apache Airflow is initialized, start the remaining services using the command:

  ```
  docker compose up
  ```

## Running the Pipeline

- After starting the services, you can access the Airflow webserver at `localhost:8080`.
- In the Airflow interface, you will find a Directed Acyclic Graph (DAG) representing your pipeline.
- You can manually trigger the DAG to execute the ELT pipeline.
- Once executed, you can verify the updated data models in the `destination_postgres` database.

## Accessing Docker Container

- To access the Docker container on the terminal, use the following command:

```
docker exec -it etl-destination_postgres-1 psql -U postgres
```


- After logging in, you can check the `destination_db` by connecting to it:

```
\c destination_db
\dt
```

This setup enables efficient data processing through the ELT pipeline, integrating Dbt, Docker, and Apache Airflow seamlessly.

