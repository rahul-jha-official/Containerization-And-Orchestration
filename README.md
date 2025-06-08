# Containerization-And-Orchestration
## Table of Contents
- [Bare Metal Deployment](#bare-metal-deployment)
- [Virtualization](#virtualization)
- [Containerization](#containerization)
- [Docker](#docker)


## [Bare Metal Deployment](#bare-metal-deployment)
Deploying applications on a system.

![Deploying Process](https://github.com/user-attachments/assets/0ecf7388-e2e4-473f-b48f-039c84a7791e)

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/cd23c7ad-a0e8-4315-9864-a2403366e81e" width="260px"></td>
    <td>
     Issues with Such Deployment:<br><br>
        - OS/.NET runtime version mismatch<br>
        - Missing files/settings<br>
        - Not enough hardware resources<br>
        - Dependency conflicts<br>
        - Missing Permissions<br>
        - Hardcoded paths<br>
        - Ports already in use<br>
        - Not enough servers<br>
        - Wasted hardware resources<br>
        - Very slow provisioning (hours/days)<br>
        - How to rollback ?<br>
    </td>
  </tr>
</table>

## [Virtualization](#virtualization)
Virtualization is a technology that allows multiple virtual machines (VMs) to run on a single physical machine. It creates a simulated or virtual computing environment, enabling organizations to share resources, improve efficiency, and reduce costs. 

<img src="https://github.com/user-attachments/assets/ca7df228-5b5d-4ded-b1ff-c374c29a2b8f" width = "300px" align="center">

<br><br>

| Benefit | Issues |
|--|--|
| OS/Runtime match | Significant RAM/Disk Overhead |
| Clean Environment | VM image creation pain (hour) |
| Better resource allocation | VM Provisioning too slow (minutes) |
| Built-in permissions | Boot time too slow (minutes) |
| Predictable Paths | Only so many VMs per server |
| Easier to Scale | Wasted Resources |
| Faster Provisioning | Multiple OS instances to patch |
| Simpler Rollback | Hard to version control VM images |

### Hypervisor
Hypervisor is a software that lets you to create and run multiple virtual machines; where each virtual machine can have its own operating system based on pre-allocated hardware resources.

Issues: 
- Manual effort to replicate environment.
- Large foot-print and wastage of hardware resources.
- Error-prone due to config mismatches, differences in versions of dependencies, missing dependencies or other human-errors.
- Difficult to scale-out as it needs substantial investment in hardware resources.

## [Containerization](#containerization)
Containerization is a lightweight form of operating system virtualization that allows you to package an application along with everything it needs to run—like libraries, dependencies, configuration files—into a single, portable unit called a container.

<img src="https://github.com/user-attachments/assets/8176443f-998c-4398-b09b-c88c2e40f0f5" width= "300px">

### Benefits of Containerization
- **Isolation** - Containers provide a level of isolation for applications, preventing conflicts with other applications or the host system. Each container operates independently, enhancing security and reliability.
- **Portability** - Containers encapsulate applications and their dependencies, ensuring consistency across various environments. This portability enables developers to build, test, and deploy applications seamlessly across different platforms.
- **Resource Optimization** - Containers share the host OS's kernel and use resources more efficiently than traditional virtual machines. This allows for higher density on a given host, optimizing resource usage.
- **Consistency** - Containers include everything needed to run an application, from compiled-code to dependencies. This ensures consistency between development, testing, and production environments, reducing the likelihood of "it works on my machine" issues.
- **Scalability** - Using containers with microservices lets you easily scale specific parts of your application by running each service in its own container, offering flexibility and efficient resource utilization.
- **Faster Deployment** - Containers can be started and stopped quickly, enabling rapid deployment and scaling of applications. This speed is crucial for modern development practices like continuous integration and continuous deployment (CI/CD).
- **Version Control** - Docker images can be versioned, allowing developers to track changes, roll back to previous versions, and maintain a history of application states.

### Container vs Virtual Machine
| Feature | Virtual Machine | Container |
|--|-- |--|
| **Isolation** | Provide strong isolation by virtualizing the entire operating system. | Offer lightweight isolation, sharing the host OS's kernel, resulting in less overhead and faster startup times. |
| **Resource Usage** | Require more resources due to running a full OS for each VM. | Use fewer resources by sharing the host OS kernel, leading to higher density and efficiency. |
| **Performance** | Tend to have slightly higher overhead and longer startup times. | Have lower overhead and faster startup, promoting rapid scaling and deployment. |
| **Scaling** | Scale by deploying additional virtual machines, which can be slower. | Scale more quickly, allowing independent scaling of microservices. |
| **Deployment Speed** | Typically have longer deployment times due to the need to boot an entire OS. | Deploy quickly since they only need to start the application and its dependencies. |
| **Use Cases** | Suitable for running different operating systems on the same hardware. | Ideal for microservices architectures, where services can run in isolated containers. |
| **Overhead** | Have higher overhead because of the need for separate OS instances. | Have lower overhead, making them more lightweight. |

### Host Operating System
OS devided into two component:
- OS Kernel
- OS User Space

**OS Kernel** <br>
OS Kernel is core part of Operating System that directly controls hardware resources (Memory, Schedules, Processes, Talk to devices and enforces Security).<br>

**OS User Space**<br>
OS User Space is the space where most system services and your application lives. Program here can't access hardware directly, they need to go through OS Kernel. This separation keeps your system stable and secure.<br>

### Container Runtime
A container runtime is a low-level software component that creates, runs, and manages containers on a host system.

A container runtime is responsible for:
- Pulling container images from a registry (e.g., Docker Hub)
- Unpacking the image layers into a container
- Creating isolated environments using Linux features like:
  - Namespaces (for process, network, file system isolation)
  - Cgroups (for limiting CPU, memory, etc.)
- Running the containerized application
- Managing container lifecycle (start, stop, restart, remove)

### Why Virtualization is Containerization is so efficient ?
Most production environments use both:
- Use virtual machines for isolation and security at the infrastructure layer.
- Run containers inside those VMs for fast, scalable application deployment.


<img src="https://github.com/user-attachments/assets/85609d49-2fa8-43b4-97a9-eb35cde26bb1" width= "300px">

Analogy: Think of a VM as a house, and a container as a room in that house. If you want full control, including different plumbing and electrical systems (different OS), you need separate houses. But if all your applications can share the same systems, rooms are much more efficient.


## [Docker](#docker)
Docker is a containerization tool that packages applications with their dependencies for consistent and efficient deployment across diverse environments.

### Docker Desktop Architechture 
- WSL (Windows Subsystem for Linux) is a compatibility layer for running Linux natively on Windows, without using a virtual machine or dual boot. WSL lets developers run a real Linux environment (bash shell, command-line tools, even Docker) directly on Windows, side-by-side with their Windows applications.
  - WSL 1 - Translation layer (no Linux kernel). Uses Windows NT kernel. Good Performance.
  - WSL 2 - Lightweight VM with real Linux kernel. Full Linux Kernel. Excellent Performance.
- Docker API: The Docker API is a RESTful interface that allows you to programmatically control Docker—including actions like creating containers, pulling images, and managing networks or volumes. You can use the Docker API to:
  - Automate container operations
  - Build custom tools or dashboards
  - Integrate Docker into CI/CD pipelines
- The Docker Daemon (dockerd) is the core background service of Docker that manages everything: containers, images, networks, and volumes. It listens for Docker API requests and executes them. It manages container lifecycle and interacts with the host OS. It's a long-running process on your system. It communicates with:
  - The Docker CLI (docker commands)
  - Other tools (like Docker Compose, Docker API clients)
  - The container runtime (e.g., containerd and runc)

![image](https://github.com/user-attachments/assets/b13a0727-922d-4cee-8fbc-0cd5da0dedd3)


### Docker Image
A self-contained package with all the components needed to run a software application, such as code, dependencies, and environment settings.

### Docker Container
A lightweight, isolated, and executable instance created from a Docker image.

### Docker Tag
A tag is a label applied to a specific version of a Docker image within a repository. It helps differentiate different versions or configurations of the same application.

<img src="https://github.com/user-attachments/assets/80727454-55e0-478c-9a86-8c4ad750a28a" width="300px">

### Docker Volumne
The persistent storage for docker.

<img src="https://github.com/user-attachments/assets/123f77f7-d5b9-4da8-a812-87923e2d95aa" width="300px">

### Docker Port Mapping
The docker container run in an isolation. So the port of the container is also isolated to system. To interact we have to map the port.

<img src="https://github.com/user-attachments/assets/f344478b-1e50-4ac3-a434-46460ad6bc4d" width="300px">

### Docker Networks
A Docker network is a virtual network interface that enables communication between Docker containers.

**Docker Network Drivers**

- **Bridge**: This is the default network driver in Docker. It creates an internal network on the Docker host to which containers can connect. Containers on the same bridge network can communicate with each other using their own IP addresses.
- **Host**
- **None**
- **Overlay**
- **Macvlan**

### Dockerfile
Images are created using Dockerfiles, which specify the steps to build the image, including copying files, installing dependencies, and configuring settings.

```Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY published/ ./
ENTRYPOINT [ "dotnet", "GreetingAPI.dll" ]
```

| Command | Description | Syntax |
|--|--|--|
| `FROM` | Specifies the base image for the container | `FROM <image>:<tag>` |
| `USER` | Specifies the user that should be switched to, before executing subsequent commands | `USER <user_name_or_id>` |
| `WORKDIR` | Sets the working directory (in the image file system) | `WORKDIR <path>` |
| `EXPOSE` | Informs Docker that the container will listen to the specified internal port at run time | `EXPOSE <port>` |
| `ARG` | Defines variables that can be used within the build process or can be passed via "docker build" command | `ARG <variable_name>=<default_value>` |
| `COPY` | Copies specifies files or directories from the host machine into the image | `COPY <source_path> <destination_path>` |
| `RUN` | Executes the specified command during the build process | `RUN <command>` |
| `ENTRYPOINT` | Specifies the primary command to be run when a container is started | `ENTRYPOINT ["executable", "arg1", "arg2", …]` |

### Multi-Stage Dockerfile
Multi-stage Dockerfile is a technique while helps in optimizing the final image size by creating intermediate images and eliminating unnecessary build artifacts.

```Dockerfile
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY . .
RUN dotnet publish "GreetingAPI.csproj" -o /published /p:UseAppHost=false

FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app
COPY --from=build /published .
ENTRYPOINT [ "dotnet", "GreetingAPI.dll" ]
```

### Docker Ignore file
The docker ignore file is the file contains the list of files to exclude in the final image. The file should be named .dockerignore.

```.dockerignore
**/bin
**/obj
**/Properties
**/Dockerfile
**/.dockerignore
**/appsettings.Development.json
**/*.sln
```

### Docker Hub Repositories
1. Public Repository
- **Visibility:** Images in a public repository are visible to everyone. Anyone can search for, pull, and use these images.
- **Collaboration:** Public repositories are suitable for open-source projects or scenarios where you want to share your containerized application with a broad audience.
- **Free Access:** Typically, public repositories on Docker Hub are free to use.

2. Private Repository
- **Visibility:** Images in a private repository are restricted, and access is controlled. Only authorized users can view or pull images from a private repository.
- **Security:** Private repositories are essential for sensitive or proprietary applications where you want to control who can access and use your container images.
- **Paid Access:** Private repositories often come with subscription fees. You may need a paid plan to create and manage private Docker images.\

Note: <a href="https://hub.docker.com/" target="_blank">Link to Docker Hub</a>

### Docker Commands
| Command | Description | Properties |
|--|--|--|
| `docker version` | Get Docker Version | |
| `docker info` | Get Docker Info | |
| `docker pull <image>` | Download an image from a registry | |
| `docker images` | List all images on the local machine | |
| `docker rmi <image>` | Remove an image from the local machine | - **--force**: to remove image forcefully even if it is running |
| `docker run <image>` | Create and start a container from an image | - **-d**: Run in detached mode<br>- **-p <host_port>:<container_port>**: Map ports<br>- **--name <container_name>**: Assign a name to the container<br>- **-v <host_path>:<container_path>**: Mount a volume<br> - **-rm**: Remove container once it stops |
| `docker ps` | List running containers | - **-a/--all**: Show all containers, including stopped ones |
| `docker stop <container>` | Stop a running container | |
| `docker start <container>` | Start a stopped container | |
| `docker restart <container>` | Restart a running or stopped container | |
| `docker exec -it <container> <command>` | Execute a command inside a running container | - **-it**: Interactive terminal |
| `docker logs <container>` | View logs of a container | - **-f**: Follow the log output |
| `docker build -t <image_name>:<tag> <path>` | Build a Docker image from a Dockerfile | - **-t**: Tag the image with a name and version<br>- **<path>**: Path to the directory containing the Dockerfile |
| `docker network ls` | List all Docker networks | |
| `docker network create <network_name>` | Create a new Docker network | - **--driver <driver_name>**: Specify the network driver (e.g., bridge, overlay) |
| `docker network inspect <network_name>` | Inspect a Docker network for details | |
| `docker volume ls` | List all Docker volumes | |
| `docker volume rm vol-name` | Remove volume | |
| `docker volume create <volume_name>` | Create a new Docker volume | |
| `docker volume inspect <volume_name>` | Inspect a Docker volume for details | |
| `dotnet publish .\App.csproj -o published` | for creating build | - **/p:UseAppHost=false**: for skip creation of executable file | 
