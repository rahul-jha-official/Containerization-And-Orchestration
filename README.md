# Containerization-And-Orchestration
## Table of Contents
- [Bare Metal Deployment](#bare-metal-deployment)
- [Virtualization](#virtualization)
- [Containerization](#containerization)


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

