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

## 9.2 Installing Docker on EC2

After connecting to the EC2 instance through SSH, Docker was installed using:

```
sudo yum update -y
```

```
sudo yum install -y docker
```

```
sudo service docker start
```

The EC2 user was added to the Docker group:

```
sudo usermod -a -G docker ec2-user
```

After logging out and reconnecting, Docker was verified with:

```
docker --version
```

and:

```
docker ps
```

<img width="937" height="397" alt="Captura de pantalla 2026-09-23 a la(s) 8 38 58 p m" src="https://github.com/user-attachments/assets/26e7941b-516b-447b-ba4c-d3dd8abde860" />

<img width="1188" height="216" alt="Captura de pantalla 2026-09-23 a la(s) 8 41 21 p m" src="https://github.com/user-attachments/assets/c3f7a5a7-3d42-4de8-a807-b8afd244f0d9" />


---

# 10. Deploying the Docker Image to EC2

The Docker image was downloaded directly from Docker Hub:

```
docker pull lauragutierrez12/virtualization-lab:1.0
```

The container was then started with:

```
docker run -d \
  --name virtualization-lab \
  --restart unless-stopped \
  -e PORT=9000 \
  -p 8080:9000 \
  lauragutierrez12/virtualization-lab:1.0
```

The port mapping is:

```
EC2 host:       8080
Docker container: 9000
```

The container status was verified with:

```
docker ps
```

The application logs were checked with:

```
docker logs virtualization-lab
```

<img width="630" height="155" alt="Captura de pantalla 2026-09-23 a la(s) 8 39 56 p m" src="https://github.com/user-attachments/assets/9ea8095a-0b65-4594-bf31-5cb47854a608" />



---

# 11. Public AWS Deployment

The deployed application was tested through the public DNS address of the EC2 instance.

Endpoint:

```
http://ec2-54-226-177-173.compute-1.amazonaws.com:8080/greeting?name=AWS
```

Expected response:

```
Hello, AWS!
```

The successful response confirms the following communication path:

```
Browser
  |
  | HTTP :8080
  v
AWS EC2
  |
  | Docker port mapping
  | 8080 -> 9000
  v
Spring Boot Container
  |
  v
/greeting
```
<img width="684" height="118" alt="Captura de pantalla 2026-09-23 a la(s) 8 43 34 p m" src="https://github.com/user-attachments/assets/7c6da022-0092-4e3b-948e-e6c5f5277683" />


<img width="533" height="283" alt="Captura de pantalla 2026-09-23 a la(s) 8 40 21 p m" src="https://github.com/user-attachments/assets/877b94cf-2091-4d57-bd76-f52f359c80d9" />

<img width="804" height="286" alt="Captura de pantalla 2026-09-23 a la(s) 8 40 56 p m" src="https://github.com/user-attachments/assets/d2206eca-8981-466f-8d9a-263da6a0a3ad" />

---

# 12. Deployment Architecture

The final deployment model is:

```
                 Internet
                   |
                   |
                HTTP :8080
                   |
                   v
           +----------------------+
           |       AWS EC2        |
           |     t3.micro         |
           |  Amazon Linux 2023   |
           |                      |
           |  +----------------+  |
           |  | Docker Engine   |  |
           |  |                |  |
           |  | Spring Boot    |  |
           |  | Web Container  |  |
           |  |     :9000      |  |
           |  +----------------+  |
           +----------------------+
                   |
                   |
                Docker runtime
```

For the local environment, Docker Compose provides the following architecture:

```
              Local Machine
                 |
            Docker Compose
                 |
         +-----------+-----------+
         |                       |
         v                       v
    +-------------+         +-------------+
    | Spring Boot |         |  MongoDB    |
    |    web      |         |     db      |
    |    :9000    |         |   :27017    |
    +-------------+         +-------------+
         |
         |
      Host :8087
```

---

# 13. Architecture Responsibilities

## Client

The client sends HTTP requests to the public EC2 endpoint.

Example:

```
/greeting?name=AWS
```

## EC2

Amazon EC2 provides the virtual machine where Docker is executed.

It provides:

- Compute resources.
- Network connectivity.
- Public access through the configured security group.
- Storage through EBS.

## Security Group

The Security Group controls inbound network access.

The deployment allows:

```
TCP 22   -> SSH administration
TCP 8080 -> Web application
```

Other unnecessary ports are not exposed.

## Docker

Docker provides the container runtime used to isolate and execute the Spring Boot application.

## Spring Boot

The Spring Boot application processes HTTP requests and returns the greeting response.

---

# 14. Cost Analysis

The cost analysis considers a single continuously running EC2 instance and three monthly request scenarios:

```
10,000 requests/month
100,000 requests/month
1,000,000 requests/month
```

## Assumptions

For the baseline calculation:

| Parameter | Assumption |
|---|---|
| AWS Region | US East (N. Virginia), us-east-1 |
| EC2 instance | t3.micro |
| Instances | 1 |
| Runtime | 730 hours/month |
| EBS | 8 GiB gp3 |
| Public IPv4 | 1 |
| Application | Single Docker container |
| Load balancer | Not included |
| Managed database | Not included |
| Monitoring | Not included |
| Backups | Not included |
| Data transfer | Assumed low enough not to materially change this baseline |
| Availability | Single instance, no high availability |

The EC2 t3.micro on-demand example for `us-east-1` is approximately `$0.0104/hour`. AWS documentation also lists gp3 storage at approximately `$0.08/GiB-month` for the referenced US East pricing example. Public IPv4 addresses are charged separately at `$0.005/hour` when applicable. These values should be cross-checked with the AWS Pricing Calculator at the time of submission.

### Baseline monthly estimate

EC2 compute:

```
$0.0104 × 730 hours
= $7.592/month
```

8 GiB gp3 EBS:

```
$0.08 × 8 GiB
= $0.64/month
```

One public IPv4 address:

```
$0.005 × 730 hours
= $3.65/month
```

Estimated infrastructure baseline:

```
$7.592 + $0.64 + $3.65
= $11.882/month
```

Rounded:

```
≈ $11.88/month
```

This is an illustrative baseline and does not include account-specific Free Tier credits, taxes, additional AWS services, significant data transfer, or other charges.

## Cost per Request

The workshop formula is:

```
Cost per request =
Monthly infrastructure cost / Monthly requests
```

Using the estimated baseline of approximately `$11.88/month`:

| Monthly Requests | Estimated Monthly Infrastructure Cost | Approx. Cost per Request |
|---:|---:|---:|
| 10,000 | $11.88 | $0.001188 |
| 100,000 | $11.88 | $0.0001188 |
| 1,000,000 | $11.88 | $0.00001188 |

The important characteristic of this calculation is that the basic EC2 infrastructure cost is largely independent of the number of requests while the instance remains running continuously. Therefore, the infrastructure cost per request decreases as the request volume increases.

The final submitted cost analysis should include the screenshot or exported result from the AWS Pricing Calculator.

---

# 15. Cost Analysis Discussion

## Why is there a baseline monthly cost even with very few requests?

The EC2 instance consumes infrastructure resources while it is running. The application can receive very few requests and still incur compute, storage, and potentially public IPv4 costs.

Therefore, a continuously running virtual machine has a relatively fixed infrastructure component.

## Why does the cost per request decrease as traffic increases?

The same running infrastructure can process many requests.

For example, if the monthly infrastructure cost remains approximately constant:

```
10,000 requests
      |
      v
Higher cost per request
```

while:

```
1,000,000 requests
      |
      v
Lower cost per request
```

The infrastructure is being utilized by a larger number of requests.

## What would require multiple EC2 instances?

Multiple instances may be required when a single instance is no longer sufficient for the workload or when the architecture requires higher availability.

Possible reasons include:

- Increased CPU utilization.
- Increased memory consumption.
- Higher concurrent request volume.
- Need for horizontal scaling.
- High availability requirements.
- Fault tolerance.
- Maintenance without taking the service completely offline.

## What additional services would normally be considered in production?

A production architecture could require additional services such as:

- Load balancer.
- Multiple EC2 instances.
- Auto Scaling.
- Managed database.
- Monitoring and logging.
- Backups.
- Container registry.
- HTTPS/TLS.
- DNS.
- Network security controls.

These services would increase the total infrastructure cost.

## Would serverless necessarily be cheaper?

The answer depends on the workload.

For workloads with low or intermittent traffic, a serverless architecture may avoid paying for an always-running virtual machine because resources can be consumed based on executions.

For continuously active workloads, the economics can be different because a continuously running EC2 instance spreads its fixed infrastructure cost across a larger number of requests.

Therefore, the appropriate architecture depends on workload characteristics such as:

- Request frequency.
- Execution duration.
- Resource consumption.
- Traffic variability.
- Availability requirements.
- Operational requirements.

---


## Public Deployment

Evidence of the browser response:

```
Hello, AWS!
```

from the EC2 public endpoint.

<img width="795" height="221" alt="Captura de pantalla 2026-09-23 a la(s) 8 42 12 p m" src="https://github.com/user-attachments/assets/26e79ed7-7254-4807-887f-2b2c03bce42f" />

<img width="1160" height="214" alt="Captura de pantalla 2026-09-23 a la(s) 8 42 31 p m" src="https://github.com/user-attachments/assets/1cddfc8a-75cd-46df-96fd-f88393adf20b" />


## Architecture

Evidence of the deployment model diagram.
