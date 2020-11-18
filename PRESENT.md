---
title: An introduction to Docker
author: Jochen Van de Voorde
purpose: Python bootcamp, Ordina Belgium nv, december 2020
...

# A very short Quiz

A group of whales is called a 

. . .

pod!

# Verify Docker installation

```
docker version
```

or

```
docker --version
```

# Your trainer today

Jochen Van de Voorde

* @Ordina since July 2006
* switched to VisionWorks in 2016 (prev JWorks)
* tech: Python, Scala, Go(lang), Docker, Kubernetes, AWS, Airflow, Apache Spark, ...

recent projects:

* Port of Rotterdam: "Navigate" - container orchestration (pun intended)
* Arcelor Mittal: on premise Hadoop setup and streaming data ingest with Kafka
* DPG Media (present) - video recommendations for VTMGo, Streamz, HLN, AD

# Relevance - skills in demand (1)

_Skills & Qualifications_

For the **Big Data Position**:

* You have experience with some main AWS services like Lambda functions, Athena,
EMR, Redshift, ElasticSearch, Lake Formation, Kinesis, Amazon QuickSight, S3,
Glue.
* You've worked with some of the following tools Apache Hadoop, Spark, **Docker**,
CI/CD
* You are good with one of the Java / Scala / Python
* Most important of all the above: You need to be a good cultural fit. That's a
motivated and career-driven individual who can work in an entrepreneurial
environment, surrounded by highly-skilled colleagues who always come up with
innovative ideas.
* You must be fluent in Dutch or French + English.

. . .

_Desired Skills & Experience_

Required:

* Master or Phd in computer science or related field
* At least 2 years of experience in software engineering in a data context
* Programming experience with one or more languages: Python, Scala, Java, C/C++,
* Knowledge of relational database technologies/concepts and SQL is required
* Solid understanding of Linux
* In depth knowledge of at least one cloud provider (GCP, AWS or Azure).
* Certifications from any of these is considered a plus.
* Familiarity with big data technologies such as Apache Spark, ElasticSearch, ...
* Experience with containers and container orchestration (**Docker**, Kubernetes, )
* Able to coach others and give technical advice and direction
* Able to work independently, prioritize multiple stakeholders and tasks, and manage
work time effectively.
* Proficient in English, knowledge of Dutch and/or French is a plus.

# Relevance - skills in demand (2)

Profiel:

* Je hebt een bachelor of master in een wetenschappelijke richting (ingenieur,
informatica, wetenschappen, ...)
* Je hebt ervaring in **Data Engineering** of je bent zeer sterk gemotiveerd om hier
mee je schouders onder te zetten
* Ervaring met Data Science in de medische wereld is een pluspunt;
* Ervaring in een ETL / ELT omgeving en het opzetten en beheer van een Data
Warehouse / Data Lake is zeker een meerwaarde
* Je bent vertrouwd met de principes en methoden van software ontwikkeling, en
kan die toepassen op Python gebaseerde data pipelines
* Je hebt een praktische kennis van Java en Python, je hebt gewerkt met Pandas,
NumPy, scikit-learn of een soortgelijke API, en kennis van SQL is natuurlijk een
must
* Je hebt een sterke technische bagage en bent vertrouwd met o.a. Linux, **Docker**,
Git
Je weet van aanpakken en je bent gedreven door concrete resultaten;
Je bent analytisch, je hebt goede communicatieve vaardigheden, je bent een
teamplayer en je kan ook goed zelfstandig werken;
Je draagt privacy en ethiek hoog in het vaandel.

. . .

Profiel:

* Je hebt minimum 5 jaar relevante werkervaring
* Je bent communicatief en een teamspeler
* Je bent analytisch, kritisch en denkt out of the box
* Je hebt ervaring met data privacy (GDPR) implementaties
* Je volgt technologische ontwikkelingen op de voet en kan hype van
* waarde onderscheiden
* Je hebt kennis van gestructureerde en ongestructureerde datavormen
* Je hebt ervaring met monitoring en logging op AWS
* Je hebt een goede kennis van Linux, Bash scripting, Python en/of Scala,
Spark, Terraform, **Docker**, een CI/CD framework
* Kennis van Airflow, Databricks of Jupyter, Kubernetes is een plus
* Je hebt een geldig en relevante AWS certificatie
* Je communiceert vloeiend in het Nederlands en Engels

# Relevance - technical

Who can relate to these statements?

. . .

_"It works on my pc"_

. . .

_"Installation failed. module requires version >1.11, but you have 1.10"_

. . .

_"Module not found: numpy"_

. . .

_“It works for me, what version are you on?”_

. . .

_"Yeah, it only works on Mac"_

. . .

_"I'm a Data Scientist / Engineer, I don't need this"_

...

# The problem

we build:

* (data) applications

should _just work_:

* libraries and dependencies
* Operating System
* Infrastructure

. . .

# Solution #1

Virtual Machines (VMs)

>A virtual machine (VM) runs a full-blown “guest” operating system with virtual access to host resources through a hypervisor. In general, VMs incur a lot of overhead beyond what is being consumed by your application logic.

```
App 1       App 2       App N
Bins/Libs   Bins/Libs   Bins/Libs
Guest OS    Guest OS    Guest OS
=================================
           Hypervisor
---------------------------------
         Infrastructure
```

# Next problem

Microservices!

Our application:

* API
* backup API for High Availability
* load balancer
* user interface
* database
* message queue
* message consumers
* authentication service
* an admin dashboard
* monitoring
* logging service

# Solution #2

Cloud platforms provide managed services!

To an extent...

E.g. **AWS** services

* API
* backup API for High Availability
* load balancer (ALB)
* user interface
* database (RDS)
* message queue (SQS)
* message consumers
* authentication service
* an admin dashboard (misc)
* logging & monitoring (CloudWatch)

Some options remain...

# Microservices, continued

We could have N applications

We want

* small footprint
* fast startup
* flexible resource allocation
* portability to run anywhere (remember technical relevance, earlier)
* scalability

Enter **Docker containers**

>A container runs natively on Linux and shares the kernel of the host machine with other containers. It runs a discrete process, taking no more memory than any other executable, making it lightweight.

```
App 1       App 2       App N
Bins/Libs   Bins/Libs   Bins/Libs
=================================
             Docker
---------------------------------
             Host OS
---------------------------------
         Infrastructure
```

. . .

Note:

- VM's are still useful
- every use case has its own context
- don't restrict yourself to a single perspective and think every problem can be solved the same way

# Docker Architecture

## `dockerd` daemon

* Listens for API requests on your or a remote system that has `dockerd` installed
* Manages Docker objects

. . .

## `docker` Client

Provides user interaction with a `dockerd` daemon

. . .

## Docker registries

* Stores Docker images
    * public: Docker Hub
    * cloud providers: AWS ECR, Azure Container Registry, ...

# Docker objects - Images

* read-only template with instructions for creating a Docker container
* layered
* can be based on other images
* defined in a `Dockerfile`
    * each instruction creates a layer
    * when you change the Dockerfile, only modified layers are rebuilt
        * optimization

```bash
docker images
```

A very simple Dockerfile

```bash
FROM ubuntu

RUN apt-get update && \
    apt-get install gcc -y
```

Oh noes linux /o\

Let's build the image

```bash
docker build -t kiss .
```

Show

```bash
docker images | grep kiss
```

Note the `tag`, relevant when pushing/pulling specific versions of an image to/from a Docker registry.

# Docker objects - Containers

- a runnable instance of a Docker image
- create, start, stop, remove, add storage, network, create an image from a container state
- can be isolated connected to other containers, part of a container orchestration platform (cf also `docker-compose`, `kubernetes`, out of scope for this intro)

```
docker container ls [-a]
```

How about that _kiss_ container? None yet

```bash
docker container ls | grep kiss
```

Let's create one

```bash
docker run -ti kiss /bin/bash
```

Note

* containers run as `root` unless otherwise specified in the Dockerfile
* no persistence (yet)

# Bookmarks

https://docs.docker.com/reference/

Today:

https://docs.docker.com/engine/reference/commandline/run/

# Exercise 1

Run a python container and run the python code

```python
print("hello container")
```

in that container.

Use the `python:3.8-slim` image.

# Exercise 2
# Exercise 3
# Exercise 4
# Exercise 5
# Exercise 6
# Exercise 7
# Exercise 8