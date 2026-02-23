## The Need for Sharing Hardware Safely and Efficiently

Virtualization introduced a new concept:

“What if multiple applications could safely share the same physical server?”

To achieve this, a virtualization layer called a **hypervisor** was introduced. The hypervisor acts as an intermediary between virtual machines and the underlying hardware, ensuring that each virtual machine operates independently, as if it were a separate physical computer.

Each virtual computer, known as a Virtual Machine (VM), acts as an independent system with its own operating system, apps, and settings, even though they all share the same physical hardware underneath.

## Virtualization Components

### **Hypervisor**

A hypervisor is the core technology behind virtualization. It is the software responsible for creating and managing virtual machines.

A hypervisor:

- Divides a physical computer into multiple virtual machines
- Allocates dedicated portions of CPU, memory, and storage to each virtual machine
- Maintains isolation between virtual machines to ensure security and stability
- Manages the lifecycle of virtual machines (start, stop, pause, clone, delete)

Hypervisors are implemented in two main types, each suited for different scenarios, ranging from home labs to enterprise data centers.

### Type 1 Hypervisor
Runs directly on physical hardware.  
It is highly efficient and optimized for performance, making it ideal for servers and enterprise environments.

### Type 2 Hypervisor
Runs on top of an existing operating system.  
It is easier to install and configure, making it suitable for learning, testing, and small-scale environments.

### Use Case Comparison

Although most use cases can technically run on either type, some scenarios are better suited to a specific hypervisor type based on performance, security, and stability requirements.

| Use Case              | Type 1 | Type 2 |
|-----------------------|--------|--------|
| Test malicious files  |        | X      |
| Production server     | X      |        |
| Database server       | X      |        |
| Software testing      |        | X      |
| Kali Linux lab        |        | X      |
| Data center           | X      |        |

---

When using virtualization to test malicious files, special care must be taken to prevent the host system from becoming infected by malware running inside the guest machine.

Recommended precautions include:

- Using different operating systems for the host and guest
- Isolating the guest machine from the host network
- Disabling shared folders and clipboard sharing
- Avoiding direct communication between host and guest

## Virtual Machines 

A **Virtual Machine (VM)** is a virtual computer created and managed by a hypervisor.

Although virtual, a VM behaves like a physical machine:

- It has its own virtual CPU, RAM, storage, and network interfaces.
- It can run any operating system (Windows, Linux, etc.).
- It operates independently from other VMs. If one VM fails, the others continue running unaffected.

You can deploy virtual machines on your personal computer using tools such as **Oracle VirtualBox** or **VMware Workstation**. These tools function as Type 2 hypervisors, allowing you to run multiple operating systems — such as Windows, Linux, or macOS — on a single physical machine.

## Containers 

A **container** is a lightweight, isolated environment designed to run a single application along with all the components required for it to function.

Unlike a virtual machine, a container does not include a full operating system. Instead, it shares the host system’s kernel, the core component of the operating system responsible for managing hardware resources, memory, and processes.

Because containers share the host kernel:

- They start much faster than full virtual machines.
- They consume fewer system resources.
- They must be compatible with the host operating system (e.g., a Windows container cannot run on a Linux host without additional compatibility layers).

Containers behave like self-contained environments because:

- They package the application and its dependencies (libraries, tools, specific versions).
- They share the host operating system, enabling near-instant startup.
- They remain isolated from other containers, so a failure in one container does not directly impact others.
- They provide consistent execution across different environments, making them ideal for development, testing, and scalable deployments.

The most common platform for deploying containers is **Docker**.

Docker is an open-source platform that simplifies the process of building, packaging, deploying, and running applications using containerization technology.