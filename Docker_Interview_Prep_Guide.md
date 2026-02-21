# Docker -- Structured Interview Preparation Guide

Author: Revision Notes\
Purpose: Complete conceptual + practical Docker reference for interviews
and GitHub documentation.

------------------------------------------------------------------------

# 1. What is Docker?

Docker is a containerization platform that packages an application along
with its dependencies into a container.\
It ensures consistent execution across development, testing, and
production environments.

------------------------------------------------------------------------

# 2. Why Docker is Used

-   Eliminates environment mismatch issues
-   Lightweight alternative to Virtual Machines
-   Faster startup time
-   Efficient resource utilization
-   Supports microservices architecture
-   Easy CI/CD integration

------------------------------------------------------------------------

# 3. Architecture Overview (Diagrams Section)

## 3.1 Docker High-Level Architecture

    +-------------------+
    |   Docker Client   |
    +-------------------+
              |
              v
    +-------------------+
    |   Docker Daemon   |
    +-------------------+
              |
      -----------------------
      |          |          |
      v          v          v
    Images   Containers   Volumes

## 3.2 Virtual Machine vs Docker

Virtual Machine:

    +-------------------+
    |   Application     |
    +-------------------+
    |   Guest OS        |
    +-------------------+
    |   Hypervisor      |
    +-------------------+
    |   Host OS         |
    +-------------------+

Docker:

    +-------------------+
    |   Application     |
    +-------------------+
    |   Docker Engine   |
    +-------------------+
    |   Host OS Kernel  |
    +-------------------+

------------------------------------------------------------------------

# 4. Dockerfile vs Docker Image

Dockerfile: - Blueprint - Text file - Contains build instructions

Docker Image: - Built artifact - Immutable - Used to create containers

------------------------------------------------------------------------

# 5. Important Dockerfile Instructions

FROM -- Base image\
WORKDIR -- Set working directory\
COPY -- Copy files\
ADD -- Copy + extract\
RUN -- Execute command during build\
CMD -- Default command\
ENTRYPOINT -- Main executable\
EXPOSE -- Document port\
ENV -- Runtime environment variable\
ARG -- Build-time variable\
VOLUME -- Define mount point

CMD vs ENTRYPOINT: - ENTRYPOINT defines executable - CMD defines default
arguments

------------------------------------------------------------------------

# 6. Docker Image Layers

Each Dockerfile instruction creates an immutable layer.

Benefits: - Layer caching - Faster rebuilds - Shared storage efficiency

Best Practice: Install dependencies before copying application code to
leverage caching.

------------------------------------------------------------------------

# 7. Docker Run vs Start vs Exec

docker run: - Creates new container - Starts container - Can configure
ports, volumes, environment

docker start: - Starts existing stopped container - Cannot modify
configuration

docker exec: - Runs command inside running container

------------------------------------------------------------------------

# 8. Detached vs Attached Mode

Attached Mode: docker run nginx

Detached Mode: docker run -d nginx

------------------------------------------------------------------------

# 9. Port Binding

docker run -p 8080:80 nginx

Host Port 8080 → Container Port 80

Note: EXPOSE only documents port. It does not publish it.

------------------------------------------------------------------------

# 10. Docker Volumes (Detailed)

Purpose: Persistent data storage outside container filesystem.

Types:

1.  Named Volume docker volume create mydata docker run -v mydata:/data
    nginx

2.  Bind Mount docker run -v /host/path:/container/path nginx

3.  Anonymous Volume

Properties: - Survives container deletion - Can be shared across
containers - Stored locally under /var/lib/docker/volumes/ (Linux)

For central/shared storage: - Use NFS - Cloud storage - Volume drivers

------------------------------------------------------------------------

# 11. Docker Networks

Default Types: - bridge - host - none - custom

Docker Compose automatically creates a default bridge network.

Containers communicate using service name as hostname.

------------------------------------------------------------------------

# 12. Docker Compose

Used for multi-container applications.

Example:

version: "3" services: app: build: . ports: - "8080:8080" db: image:
mysql

Command: docker compose up -d

------------------------------------------------------------------------

# 13. Practical Command Examples Section

## Build Image

docker build -t myapp:1.0 .

## Run Container

docker run -d -p 8080:80 myapp:1.0

## View Running Containers

docker ps

## View All Containers

docker ps -a

## Stop Container

docker stop container_id

## Remove Container

docker rm container_id

## Remove Image

docker rmi image_id

## View Logs

docker logs container_id

## Enter Running Container

docker exec -it container_id bash

## Inspect Container

docker inspect container_id

## View Resource Usage

docker stats

------------------------------------------------------------------------

# 14. Publishing Image to Docker Hub

docker login\
docker tag myapp username/myapp:1.0\
docker push username/myapp:1.0

------------------------------------------------------------------------

# 15. Changing Container Configuration

Containers are immutable.

To change: - Ports - Volumes - Environment variables - Networks

Modify docker-compose.yml and recreate:

docker compose up -d --force-recreate

------------------------------------------------------------------------

# 16. Troubleshooting Strategy

If container stops unexpectedly: 1. Check logs → docker logs
container_id 2. Check status → docker ps -a 3. Inspect configuration →
docker inspect container_id 4. Enter container → docker exec -it
container_id sh

------------------------------------------------------------------------

# 17. Interview Rapid Revision Points

-   Image is immutable
-   Container is runtime instance
-   run = create + start
-   exec works only on running container
-   Volumes prevent data loss
-   Compose auto-creates network
-   EXPOSE does not publish port
-   Configuration change requires recreation

------------------------------------------------------------------------

End of Document
