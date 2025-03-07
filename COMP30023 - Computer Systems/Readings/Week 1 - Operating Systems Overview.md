
# Defining the OS
Operating systems acts both as *extended machines* and *resource managers*
- Extended machines -> hardware abstractions, simple interfaces
- Resource managers -> Space and time multiplexing

# Processor Architecture
[[L2 - Operating System Overview#Computer Architecture|Lecture Notes]]

**Summary**:
- Contain general and special purpose registers
- Work on clock cycles to decode and execute instructions from program memory
- Perform computations in the ALU, memory lookups in MMU


# Memory Architecture
[[L2 - Operating System Overview#Computer Architecture|Lecture Notes]]

Memory is tiered:
- Registers (very temporary/volatile/shared)
- Cache (L1-3)
- Main Memory (Partitioned via address spaces)

Address spaces also permit the use of *virtual memory*


# I/O Devices

IO Devices consist of 2 parts:
- The *controller*
- The *device itself*



# Processes
A process is essentially a program in execution
Each process has an associated address space

>[!cite]
A process is fundamentally a container that holds all the information needed to run a program.

In many operating systems information about each process is stored in a *process table*, which is an array of structures, one for each process that is currently running.

As processes are able to spawn child processes, there must be a system to communicate between 'cooperating' processes.
- *Inter-process Communication* (IPC)

Processes can wait for communication (the waiting is terminated via an *alarm signal* from the operating system)
- This causes the process to suspend its current work and invoke a signal handling procedure (e.g. re-transmit a lost message if waiting for acknowledgement timed out)

