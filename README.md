# true-connector-trainning

This repository contains the docker-compose and the configuration files needed to deploy a TrueConnector in the trainning platform.
ENG TrueConnector is used, execution core and usage control provided by ENG haven´t been modified. Data App has been modified. This Data App has been extended with features that allow the acces to mlflow tracking API and Minio storage. 

## Requirements

- Linux machine with Docker version 23.0.5 or above
- Linux machine with Docker-compose version 1.29.2 or above

## Getting started

- Clone this repository.
- Move to the folder true-connector-trainning
- Edit .env file and set the endpoints to access mlflow API and MinIO API
  ```
    # mlflow configuration
    MLFLOW_TRACKING_URI=http://172.16.56.42:5000
    MLFLOW_TRACKING_USERNAME=user
    MLFLOW_TRACKING_PASSWORD=password

    # minio configuration
    MINIO_URI=http://172.16.56.42:9000
    MINIO_USERNAME=user
    MINIO_PASSWORD=password
  ```
- Login in Dockerhub using the clarusproject credentials provided by ENG
- Execute docker-compose file
```
docker-compose up -d
```

## How to use

Once docker-compose is finished, all the containers shall be up and running. To check it, write in terminal type in terminal
```
docker ps -a
```
You shall see the next services up and running:
```
                                                                                                       NAMES
e13663df302f   clarus_mlflow_data_app                            "/bin/sh -c 'java -j…"   42 hours ago   Up 42 hours (unhealthy)   0.0.0.0:8083->8083/tcp, :::                                                                                                                                8083->8083/tcp, 0.0.0.0:9008->9000/tcp, :::9008->9000/tcp                                              be-dataapp-provider
b9372f79f30f   rdlabengpa/ids_execution_core_container:v1.11.0   "/bin/sh -c 'java -j…"   42 hours ago   Up 42 hours (healthy)     0.0.0.0:8086->8086/tcp, :::                                                                                                                                8086->8086/tcp, 0.0.0.0:8889->8889/tcp, :::8889->8889/tcp, 0.0.0.0:8090->8449/tcp, :::8090->8449/tcp   ecc-provider
82a8fd9040c5   rdlabengpa/ids_uc_data_app_platoon:v1.5           "/bin/sh -c 'java -j…"   42 hours ago   Up 42 hours               8080/tcp                   
```

TrueConnector is ready to be used by the aitoolkit experiments.
Airflow dags will use this connector to read data from pilots.
Airflow dags will use this connector to register desired experiments and offer them to pilots.

## TrueConnector documentation
A complete description of TrueConnector can be found [here](https://github.com/Engineering-Research-and-Development/true-connector)