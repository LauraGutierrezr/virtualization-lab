# Virtualization Lab

## Description

This project implements a REST service developed with Java and Spring Boot and later deployed using Docker and Docker Compose.

The project makes it possible to study virtualization concepts through containers, process isolation, port publishing, and communication between services.

## Technologies

- Java 21
- Maven
- Spring Boot
- Docker
- Docker Compose
- MongoDB
- Git/GitHub
- Docker Hub

## Project Structure

```text
virtualization-lab/
├── src/
├── Dockerfile
├── compose.yaml
├── pom.xml
├── README.md
└── .gitignore
```

## Local Execution

To run the application directly with Maven:

```
mvn clean package
```

Then:

```
mvn spring-boot:run
```

The application uses port 9000.

Test endpoint:

```
http://localhost:9000/greeting?name=Pedro
```

Expected response:

```
Hello, Pedro!
```

## Building the Docker Image

First, generate the JAR file:

```
mvn clean package
```

Then, build the image:

```
docker build -t lauragutierrez12/virtualization-lab:1.0 .
```

Verification:

```
docker images
```

## Running with Docker

The application can be run with:

```
docker run -d \
  --name virtualization-lab-1 \
  -e PORT=9000 \
  -p 34000:9000 \
  lauragutierrez12/virtualization-lab:1.0
```

The application is available at:

```
http://localhost:34000/greeting?name=Container
```

## Multiple Containers

Multiple instances of the same image can be run using different host ports:

```
34000 -> 9000
34001 -> 9000
34002 -> 9000
```

Each container uses the same image but operates as an independent instance.

## Docker Compose

The project includes a `compose.yaml` file that defines two services:

- `web`: Spring Boot application.
- `db`: MongoDB database.

To start the services:

```
docker compose up -d
```

To check their status:

```
docker compose ps
```

The application is available at:

```
http://localhost:8087/greeting?name=Compose
```

## MongoDB

To access MongoDB:

```
docker compose exec db mongosh
```

Select the database:

```
use workshop
```

Insertion example:

```
db.students.insertOne({
  name: "Laura",
  course: "Virtualization"
})
```

Query:

```
db.students.find()
```

## Docker Hub

The image is published at:

```
lauragutierrez12/virtualization-lab
```

Tags:

```
1.0
latest
```

## Evidence

### Local Application

The application responds correctly through Spring Boot.
<img width="714" height="317" alt="Captura de pantalla 2026-09-23 a la(s) 3 22 13 p m" src="https://github.com/user-attachments/assets/fa6538e7-e543-47cc-925f-2a0298629b0b" />

<img width="524" height="214" alt="Captura de pantalla 2026-09-23 a la(s) 3 23 10 p m" src="https://github.com/user-attachments/assets/d01a8bc6-ccc0-45b7-b7ca-34d7b129dd7d" />


<img width="546" height="182" alt="Captura de pantalla 2026-09-23 a la(s) 3 38 35 p m" src="https://github.com/user-attachments/assets/063cd7b0-11b0-4c8a-b51b-222b2d234520" />

<img width="688" height="216" alt="Captura de pantalla 2026-09-23 a la(s) 3 40 16 p m" src="https://github.com/user-attachments/assets/b0f1a0a1-cdd1-40c2-8ad9-c9debeb8da40" />

<img width="478" height="148" alt="Captura de pantalla 2026-09-23 a la(s) 3 40 39 p m" src="https://github.com/user-attachments/assets/02a1fecc-4d84-4a73-b6cf-b950d1505eee" />





### Docker

The execution of multiple containers using different ports was verified.

<img width="1064" height="202" alt="Captura de pantalla 2026-09-23 a la(s) 3 25 57 p m" src="https://github.com/user-attachments/assets/05015259-8fd9-4090-a0e0-816e14fd11e4" />

<img width="1115" height="233" alt="Captura de pantalla 2026-09-23 a la(s) 3 25 34 p m" src="https://github.com/user-attachments/assets/bdc65d9a-ae37-40db-8524-57a361488f57" />

<img width="937" height="186" alt="Captura de pantalla 2026-09-23 a la(s) 3 36 52 p m" src="https://github.com/user-attachments/assets/8d679e8b-8b09-42a4-b78a-7d68798df4ae" />

<img width="1041" height="156" alt="Captura de pantalla 2026-09-23 a la(s) 3 39 56 p m" src="https://github.com/user-attachments/assets/dceee725-d42d-45ae-9d85-f8314e17c1ee" />




### Docker Compose

The execution of the `web` and `db` services was verified.

<img width="1039" height="169" alt="Captura de pantalla 2026-09-23 a la(s) 3 38 03 p m" src="https://github.com/user-attachments/assets/b53e9048-2b0d-46cb-af77-0e2ed12f6f14" />


<img width="1161" height="297" alt="Captura de pantalla 2026-09-23 a la(s) 3 39 15 p m" src="https://github.com/user-attachments/assets/c0673075-05db-4e0b-9750-d5a44f974ced" />

<img width="563" height="213" alt="Captura de pantalla 2026-09-23 a la(s) 3 42 09 p m" src="https://github.com/user-attachments/assets/00a37539-c7eb-4b78-af97-2b94c38c951f" />


<img width="1040" height="205" alt="Captura de pantalla 2026-09-23 a la(s) 3 41 19 p m" src="https://github.com/user-attachments/assets/433a012e-47d0-49b7-baf5-3c8e4ff3e098" />


### MongoDB

The creation and querying of information in the database was verified.

<img width="503" height="312" alt="Captura de pantalla 2026-09-23 a la(s) 3 19 49 p m" src="https://github.com/user-attachments/assets/0317ea45-bb20-4869-8634-830b720c8447" />



### Docker Hub

The image was published using the `1.0` and `latest` tags.

<img width="1433" height="386" alt="Captura de pantal la(s) 3 11 09 p m" src="https://github.com/user-attachments/assets/315d9ba8-d3bd-4789-b2ff-7f2be6c31590" />


## Architecture

```
                  Docker Compose
                       |
             +---------+---------+
             |                   |
             v                   v
       Spring Boot           MongoDB
       Web Service           Database
          :9000                :27017
             |
             |
          Host :8087
```

<img width="540" height="117" alt="Captura de pantalla 2026-09-23 a la(s) 3 42 46 p m" src="https://github.com/user-attachments/assets/a1cc680c-1f0f-4761-9c4d-f01bd48b6d60" />




## Project Status

The application has been tested locally using:

- Spring Boot
- Docker
- Docker Compose
- MongoDB

The next step is to deploy the application to an EC2 instance and perform the architecture and cost analysis.
