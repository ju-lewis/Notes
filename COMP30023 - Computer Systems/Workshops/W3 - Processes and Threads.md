
# Tutorial Questions:

## Q1. Kernel vs. User Mode
Kernel mode is an execution mode of the processor that allows it to utilise privileged instructions, such as writing to a file or accessing I/O devices. User mode is the standard mode of execution for non-OS programs that can only use regular instructions. These separate modes aid an operating system in maintaining security and smooth operation as userspace programs must make requests to a standard interface (system calls) to access privileged instructions.

## Q2. System Calls
As stated above, they are a standard interface provided by the kernel for userspace programs to perform privileged actions.

## Q3. Process State Transitions
**Missing Transition - Blocked -> Running**
This transition cannot occur as a process that has been blocked must join the ready queue to be scheduled for running.

**Missing transition - Ready -> Blocked**
This transition cannot occur as a process that isn't currently running can't trigger an event to become blocked; this requires some amount of CPU time.

## Q4. Multithreading Hypothetical
Despite creating multiple threads in software, the CPU only has 1 core to execute threads on, so you'll just get time-multiplexed concurrent execution that context switches between the threads, adding additional context switching overhead without increasing processing performance.


## Q5. Process Forking

**5a.** We create 5 processes in total
**5b.** We *explicitly* create 2 threads






