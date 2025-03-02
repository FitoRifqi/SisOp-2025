# Practice Exercises

## Question and Answer

### 1.1 What are the three main purposes of an operating system?
- **Resource Management**: Efficiently manages hardware resources like CPU, memory, and I/O devices.
- **Abstraction and Simplification**: Provides a user-friendly interface to interact with hardware.
- **Security and Protection**: Ensures system security by controlling access to resources and protecting against unauthorized use.

### 1.2 When is it appropriate for the operating system to "waste" resources?
- **Improving User Experience**: Preloading applications or caching data.
- **Fault Tolerance**: Redundant storage for data integrity.
- **Security**: Running processes in isolated environments.
- **Future Scalability**: Allocating extra resources for future growth.
- **Debugging**: Logging detailed system events.
- **Energy Efficiency**: Running hardware at lower power states when idle.
- **Not wasteful**: The benefits (e.g., reliability, security, user experience) outweigh the resource usage.

### 1.3 What is the main difficulty in writing an OS for a real-time environment?
- Ensuring tasks meet strict timing constraints.

### 1.4 Should the OS include applications like web browsers and mail programs?
- **Yes**: Simplifies user experience by bundling essential tools.
- **No**: OS should focus on managing hardware and resources, leaving applications to users.

### 1.5 How does kernel mode vs. user mode function as a form of protection?
- Kernel mode allows direct hardware access, while user mode restricts it, preventing unauthorized access and protecting the system.

### 1.6 Which instructions should be privileged?
- a, c, e, f, g, h.

### 1.7 Difficulties with protected OS memory:
- Debugging becomes harder.
- Limited flexibility for OS modifications.

### 1.8 Uses of multiple CPU modes:
- **Virtualization**: Running multiple OS instances.
- **Enhanced Security**: Additional layers of protection.

### 1.9 Using timers to compute current time:
- A timer is set to interrupt the CPU at regular intervals. The number of interrupts is counted to calculate elapsed time.

### 1.10 Why are caches useful?
- **Useful**: Speed up data access, reduce CPU load.
- **Problems**: Cache coherence, increased complexity.
- **Why not replace devices?**: Caches are volatile and expensive; devices provide persistent storage.

### 1.11 Client-server vs. peer-to-peer:
- **Client-server**: Centralized, server provides services.
- **Peer-to-peer**: Decentralized, all nodes share resources.

### 1.12 Clustered vs. multiprocessor systems:
- **Clustered**: Multiple independent machines working together.
- **Multiprocessor**: Multiple CPUs in one machine.
- **High availability**: Requires failure detection and failover mechanisms.

### 1.13 Cluster data management:
- **Shared Disk**: Direct access to disk, risk of conflicts.
- **Data Replication**: Ensures consistency but increases overhead.

### 1.14 Interrupts vs. traps:
- **Interrupts**: Hardware-triggered.
- **Traps**: Software-triggered.
- **Traps can be intentional**: For system calls or debugging.

### 1.15 Linux HZ and jiffies:
- `jiffies / HZ` gives the number of seconds since boot.

### 1.16 DMA:
- a. CPU initializes transfer, DMA manages it.
- b. DMA signals CPU when done.
- c. Can interfere if DMA uses the same bus as user programs.

### 1.17 Secure OS without privileged mode:
- **Possible**: With software-based protection.
- **Not possible**: Hardware support is essential for robust security.

### 1.18 Multi-level caches:
- Local caches reduce latency, shared caches ensure coherence.

### 1.19 Storage systems (slowest to fastest):
- f, a, c, e, d, g, b.

### 1.20 Cache coherence in SMP:
- Example: Two cores read the same memory location but have different cached values due to updates.

### 1.21 Cache coherence in:
- **Single-processor**: Less critical, managed by the OS.
- **Multiprocessor**: Requires hardware/software mechanisms.
- **Distributed**: Complex due to network latency.

### 1.22 Memory protection:
- Use hardware mechanisms like memory segmentation or paging to isolate processes.

### 1.23 Network configurations:
- a. LAN.
- b. WAN.
- c. LAN.

### 1.24 Challenges for mobile OS:
- Limited resources, battery life, diverse hardware, and user interface constraints.

### 1.25 Advantages of peer-to-peer:
- Decentralized, scalable, fault-tolerant.

### 1.26 Peer-to-peer applications:
- File sharing (e.g., BitTorrent), distributed computing, messaging.

### 1.27 Open-source OS:
- **Advantages**: Transparency, flexibility, community support.
- **Disadvantages**: Lack of official support, potential security risks.
- **Who benefits**: Developers, researchers, cost-sensitive users.
- **Who dislikes**: Enterprises needing guaranteed support.
