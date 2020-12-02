---
title: An introduction to Docker
author: Jochen Van de Voorde
purpose: Python bootcamp, Ordina Belgium nv, december 2020
...

# A very short Quiz

A group of whales is called a 

. . .

pod!

# Setup - Verify Docker installation

```bash
docker version
```

or

```bash
docker --version
```

# Setup - Github

Course material for today, clone this git repo:

    git clone https://github.com/jovv/python-bootcamp-docker

Create a github account if you don't have one already and paste you github handle in the chat

Checkout a new branch with your github handle as the branch name

    git checkout -b <your github handle>

Commit and push your exercise solutions to your branch

# Your trainer today

Jochen Van de Voorde

* @Ordina since July 2006
* switched to VisionWorks in 2016 (prev JWorks)
* tech: Python, Scala, Go(lang), Docker, Kubernetes, AWS, Airflow, Apache Spark, ...

recent projects:

* Port of Rotterdam: "Navigate" - container orchestration (pun intended)
* Arcelor Mittal: on premise Hadoop setup and streaming data ingest with Kafka
* DPG Media (present) - video recommendations for VTMGo, Streamz, HLN, AD

# Why Docker ?

# Relevance - skills in demand (1)

## Skills & Qualifications

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

## Desired Skills & Experience

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

## Profiel

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

## Profiel

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

and we expect 

* libraries and dependencies
* operating system
* infrastructure

to  _just work_

. . .

Example application:

* web server - node.js
* database - PostgreSQL
* cache - Redis

. . .

Issues:

* dependencies impact different levels, down to hardware 
* compatibility matrix ~> spaghetti
* fix one thing, break another

# Solution #1

Virtual Machines (VMs)

>A virtual machine (VM) runs a full-blown “guest” operating system with virtual access to host resources through a hypervisor. In general, VMs incur a lot of overhead **beyond** what is being consumed by your application logic.

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

* small footprint (cpu,. memory, storage)
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

# Cloud platforms

VM's _and_ containers, combining both

```
App 1       App 2       App 3       App 4         |  Container   |
Bins/Libs   Bins/Libs   Bins/Libs   Bins/Libs     |              |
---------------------   ---------------------                    |  VM
       Docker                   Docker                           |
---------------------   ---------------------                    |
         OS                      OS                              |
=============================================
                 Hypervisor
---------------------------------------------
               Infrastructure
```

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

Download an image

```bash
docker pull nginx
```

Show images on your machine

```bash
docker images
```

`tag` - relevant when pushing/pulling specific versions of an image to/from a Docker registry.

e.g. postgres:9.6

Default tag: `latest`

[postgres on docker hub](https://hub.docker.com/_/postgres/)

# Docker Images - BYO

A very simple Dockerfile

```bash
FROM ubuntu

RUN apt-get update && \
    apt-get install gcc -y
```

Let's build the image

```bash
docker build -t kiss .
```

will download the file if not present

. . .

Dockerfile:

* a sequence of instruction-arguments pairs
* each instruction creates a new **layer** in the image 
* (re-)building the same image will attempt to used cached layers
* image optimization:
    * caching
    * minimize impact possible future changes 

**layered architecture** of Docker images

```bash
docker history kiss
```

# Docker Images from Images

Our simple Dockerfile

```bash
FROM ubuntu

RUN apt-get update && \
    apt-get install gcc -y
```

is based on the ubuntu image

The ubuntu image is based on the `scratch` image

`scratch` = empty image, used to build base images or minimal images containing only a single binary

[scratch image on docker hub](https://hub.docker.com/_/scratch/)



# Docker objects - Containers

* a runnable instance of a Docker image
    * the image layers are read-only
    * the container layer is write-able
    * when modifying a file in the container that were shipped with the image, Docker creates a copy of that file in the writeable layer
* create, start, stop, remove, add storage, network, create an image from a container state
* can be isolated connected to other containers, part of a container orchestration platform (cf also `docker-compose`, `kubernetes`, out of scope for this intro)

```
docker ps [-a]
```

How about that _kiss_ container? None yet

```bash
docker ps | grep kiss
```

Let's create one

```bash
docker run -ti kiss
```

random id and name, unless specified

> for interactive processes (like a shell), you must use -i -t together in order to allocate a tty for the container process

!! containers run the image instructions as `root` unless otherwise specified in the Dockerfile

Stop:

```bash
docker stop <container id or name>
```

# Docker containers (2)

!! Running an image that has no task or process defined does nothing, it stops immediately

```bash
docker run ubuntu
```

vs 

```bash
docker run ubuntu echo Did something
```

Passing a command to a running container

```bash
docker run nginx --name execdemo
docker exec nginx cat /etc/hosts
```

Enter a running container

```bash
docker exec -ti nginx /bin/bash
```

Exit the running container with `exit` or `Ctrl`-`D`


# Bookmarks

https://docs.docker.com/reference/

https://docs.docker.com/engine/reference/commandline/run/

https://docs.docker.com/engine/reference/builder/


# Summary

## Images

docker

* images
* pull
* build
* rmi
* history

## Containers

* run
* ps [-a]
* exec
* rm




# Exercise 1

# Volumes (1)

## Volume mounting

Mount docker volumes

```bash
docker create volume my_volume

docker run -ti -v my_volume:somefolder kiss
```

Where is the folder on our host system? 

MacOS runs the docker engine in a Linux VM, we have to atach to that VM first

```bash
screen  ~/Library/Containers/com.docker.docker/Data/vms/0/tty

ls -ltrh /var/lib/docker/volumes/my_volume/_data/
```

# Volume (2)

## Bind mounting

Mount host folders into the container

```bash
docker run -ti -v $(pwd):/myfolder kiss
```

Or with the newer syntax

```bash
docker run -ti --mount type=bind,source=$(pwd),target=/myfolder
```

`pwd` = print working directory

The changes you make on the files in your host system are reflected in the container, and vice versa.

# Logs

What did I / the container do?

```bash
docker logs <container id>
```

# Exercise 2

# Cleaning up

Remember how to list containers

Note

```bash
docker ps
```

vs

```bash
docker ps -a
```

How do we get rid of the leftover containers?

"Spring cleaning"

```bash
docker container prune
```

or more specific 

```bash
docker rm <container id or name>
```

Removing images

```bash
docker rmi <image name>
```

only if there are no containers dependent on the image

# Bring your own furniture

Remember our small custom image

```bash
FROM ubuntu

RUN apt-get update && \
    apt-get install gcc -y

```

. . .

Let's add some code so it does something useful (?)

**EXAMPLE** furniture

```bash
FROM ubuntu

RUN apt-get update && \
    apt-get install gcc -y

COPY hello.sh /myscripts/
```

. . .

This moves our code to the image

We can then run the script from inside the container

But what if we want to execute our code when the container is run?


# Execute - command

Containers

* run specific tasks and processes
* stop when done or an error occurs

task/process is defined by `CMD` and/or `ENTRYPOINT` in the **Dockerfile**

CMD

* default command and/or parameters
* a Dockerfile can have multiple CMD, but only the last one will be applied

**EXAMPLE** execute

```bash
CMD ["echo", "Run by command"]
```
Note: double quotes!

if only default parameters are provide, an entrypoint should also be defined

```bash
ENTRYPOINT ["echo"]
CMD ["Run by command"]
```


# Execute - entrypoint

ENTRYPOINT

* configure a container that will run as an executable

Ground rules:

https://docs.docker.com/engine/reference/builder/#understand-how-cmd-and-entrypoint-interact

Prefer "exec" form, i.e. instruction and arguments as an array

```bash
ENTRYPOINT ["instruction", "arg1", "arg2"]
```


# Exercise 3

# Map/expose ports

3 networks

* Docker "bridge" network (172.)
* none
* host

Running an api image

**EXAMPLE** api

Runs on its own docker bridge network
For the host to access it, we want to map a host port to a container port

```bash
docker run -d --name api-demo -p 8081:8081 bootcamp-api 
```

notation `HOST_PORT:CONTAINER_PORT`


# Exercise 4

# Exercise 5

# Further practice

Fun and hands-on free course at 

[KodeKloud](https://kodekloud.com/p/docker-for-the-absolute-beginner-hands-on)
