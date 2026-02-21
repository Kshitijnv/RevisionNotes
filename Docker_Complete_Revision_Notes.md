# Docker Complete Revision Notes

------------------------------------------------------------------------

# 1. What is Docker?

Docker is a containerization platform that packages an application along
with its dependencies into a standardized unit called a container.\
It ensures the application runs consistently across development,
testing, and production environments.

------------------------------------------------------------------------

# 2. Why Docker is Used

-   Eliminates "works on my machine" issues
-   Environment consistency
-   Lightweight compared to Virtual Machines
-   Faster deployment
-   Supports microservices architecture
-   Easy CI/CD integration

------------------------------------------------------------------------

# 3. Docker Installation

-   Linux → Install Docker Engine directly (runs natively)
-   Mac/Windows → Install Docker Desktop (uses lightweight Linux VM)
    -   Windows → WSL2
    -   Mac → Hypervisor

Docker Daemon runs in background and Docker CLI communicates with it.

------------------------------------------------------------------------

# 4. Docker Image

A Docker image is a read-only template used to create containers.

Contains: - Application code - Runtime - Libraries - Dependencies -
OS-level components

Built using a Dockerfile.

------------------------------------------------------------------------

# 5. Docker Container

A container is a running instance of a Docker image.

-   Lightweight
-   Isolated
-   Shares host OS kernel
-   Has its own writable layer

Multiple containers can be created from a single image.

------------------------------------------------------------------------

# 6. Dockerfile vs Docker Image

Dockerfile: - Text file - Blueprint - Contains build instructions

Docker Image: - Built artifact - Immutable - Used to create containers

------------------------------------------------------------------------

# 7. Important Dockerfile Instructions

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

# 8. Docker Image Layers

Each Dockerfile instruction creates a new immutable layer.

Benefits: - Layer caching - Faster rebuilds - Storage efficiency -
Shared layers across images

Best Practice: Place dependency installation before copying application
code to leverage caching.

------------------------------------------------------------------------

# 9. Docker Run vs Start vs Exec

docker run: - Creates new container - Starts it - Can configure ports,
volumes, environment

docker start: - Starts existing stopped container - Cannot modify
configuration

docker exec: - Runs command inside running container - Used for
debugging

------------------------------------------------------------------------

# 10. Detached vs Attached Mode

Attached Mode: - Runs in foreground - Terminal attached

Detached Mode (-d): - Runs in background - Returns container ID

------------------------------------------------------------------------

# 11. Port Binding

Used to expose container ports to host.

Example: docker run -p 8080:80 nginx

Host Port 8080 → Container Port 80

Note: EXPOSE in Dockerfile only documents the port. It does not publish
it.

------------------------------------------------------------------------

# 12. Docker Volumes

Used for persistent data storage.

Without volume → Data is lost when container is removed.

Types:

1.  Named Volume docker volume create mydata docker run -v mydata:/data
    nginx

2.  Bind Mount docker run -v /host/path:/container/path nginx

3.  Anonymous Volume

Volumes survive container deletion.

Multiple containers can share same volume.

Named volumes are stored locally (Linux): /var/lib/docker/volumes/

For shared persistence across machines, use: - NFS - Network storage -
Volume drivers

------------------------------------------------------------------------

# 13. Docker Networks

Docker supports: - bridge (default) - host - none - custom networks

In Docker Compose, services automatically share a default network.

Containers communicate using service name as hostname.

------------------------------------------------------------------------

# 14. Docker Compose

Used to manage multi-container applications.

Defined in docker-compose.yml.

Example:

version: "3" services: app: build: . ports: - "8080:8080" db: image:
mysql

Command: docker compose up -d

Compose automatically: - Builds images - Creates network - Starts
services

------------------------------------------------------------------------

# 15. Changing Configuration of Containers

Containers are immutable in configuration.

To change: - Ports - Volumes - Environment variables - Network settings

Modify docker-compose.yml and recreate container:

docker compose up -d --force-recreate

------------------------------------------------------------------------

# 16. Publishing Image to Docker Hub

1.  docker login
2.  docker tag app username/app:1.0
3.  docker push username/app:1.0

Docker Hub is a container image registry.

------------------------------------------------------------------------

# 17. Troubleshooting Commands

docker logs `<container>`{=html}\
docker ps -a\
docker inspect `<container>`{=html}\
docker exec -it `<container>`{=html} sh\
docker stats\
docker events

If container exits immediately → Check logs first.

------------------------------------------------------------------------

# 18. Virtual Machine vs Docker

Virtual Machine: - Each VM has full OS - Heavy - Slower startup - High
resource usage

Docker: - Shares host OS kernel - Lightweight - Fast startup - Efficient
resource usage

------------------------------------------------------------------------

# 19. Key Interview Points

-   Images are immutable
-   Containers are runtime instances
-   Configuration changes require container recreation
-   Use volumes for database persistence
-   Compose creates default network automatically
-   run = create + start
-   exec works only on running container

------------------------------------------------------------------------

End of Notes
