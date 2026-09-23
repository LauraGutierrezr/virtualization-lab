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

### Docker

The execution of multiple containers using different ports was verified.

### Docker Compose

The execution of the `web` and `db` services was verified.

### MongoDB

The creation and querying of information in the database was verified.

### Docker Hub

The image was published using the `1.0` and `latest` tags.

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

## Project Status

The application has been tested locally using:

- Spring Boot
- Docker
- Docker Compose
- MongoDB

The next step is to deploy the application to an EC2 instance and perform the architecture and cost analysis.
