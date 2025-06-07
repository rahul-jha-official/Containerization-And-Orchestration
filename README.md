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

## [Docker](#docker)
Docker is a containerization tool that packages applications with their dependencies for consistent and efficient deployment across diverse environments.

### Docker Image
A self-contained package with all the components needed to run a software application, such as code, dependencies, and environment settings.

### Docker Container
A lightweight, isolated, and executable instance created from a Docker image.

### Docker Tag
A tag is a label applied to a specific version of a Docker image within a repository. It helps differentiate different versions or configurations of the same application.

### Docker Networks
A Docker network is a virtual network interface that enables communication between Docker containers.

**Docker Network Drivers**

- **Bridge**: This is the default network driver in Docker. It creates an internal network on the Docker host to which containers can connect. Containers on the same bridge network can communicate with each other using their own IP addresses.
- **Host**
- **None**
- **Overlay**
- **Macvlan**


### Docker Hub Repositories
1. Public Repository
- **Visibility:** Images in a public repository are visible to everyone. Anyone can search for, pull, and use these images.
- **Collaboration:** Public repositories are suitable for open-source projects or scenarios where you want to share your containerized application with a broad audience.
- **Free Access:** Typically, public repositories on Docker Hub are free to use.

2. Private Repository
- **Visibility:** Images in a private repository are restricted, and access is controlled. Only authorized users can view or pull images from a private repository.
- **Security:** Private repositories are essential for sensitive or proprietary applications where you want to control who can access and use your container images.
- **Paid Access:** Private repositories often come with subscription fees. You may need a paid plan to create and manage private Docker images.\



### Docker Commands
| Command | Description | Properties |
|--|--|--|
| `docker version` | Get Docker Version | |
| `docker info` | Get Docker Info | |
| `docker pull <image>` | Download an image from a registry | |
| `docker images` | List all images on the local machine | |
| `docker rmi <image>` | Remove an image from the local machine | - **--force**: to remove image forcefully even if it is running |
| `docker run <image>` | Create and start a container from an image | - **-d**: Run in detached mode<br>- **-p <host_port>:<container_port>**: Map ports<br>- **--name <container_name>**: Assign a name to the container<br>- **-v <host_path>:<container_path>**: Mount a volume<br> - **-rm**: Remove container once it stops |
| `docker ps` | List running containers | - **-a**: Show all containers, including stopped ones |
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
| `docker volume create <volume_name>` | Create a new Docker volume | |
| `docker volume inspect <volume_name>` | Inspect a Docker volume for details | |
