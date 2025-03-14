

# Multiprogramming Summary
- Process execution is interleaved
- Provides illusion of parallelism
- Allows for increased efficiency
- Scheduling algorithm determines which process gets to run next and for how long

An example of this is interleaved print results from starting multiple identical processes that just perform a busy-wait and then print a result.


# Processes

## Process Creation
Four main events that cause processes to be created:
1. System initialisation
2. Execution of a process creation system call by a running process
3. A use request to create a new process
4. Initiation of a batch job


>[!example]
>UNIX syscall `fork()`
>Creates a clone of the calling process
>- Different address spaces
>- Same memory image
>- Same values for the program counter and general-purpose registers, same open file handles.

The next instruction executed after `fork`ing a process is the next instruction *after* the fork call. i.e., PC carries over

`fork()` returns 0 in child process, non-zero in parent process.

Often, `fork()` calls are combined with calls to functions in the `exec` family to change the current process to a desired process.


## Process Termination

1. Normal exit (voluntary)
2. Error exit (Voluntary)
3. Fatal error (involuntary)
4. Killed by another process (involuntary)


## Process States
**Possible States**:
- Running - currently using the CPU
- Ready - Runnable, but temporarily stopped
- Blocked - Unable to run until some external event happens

A process transitions from running to ready when a scheduler picks another process
A process starts running when it gets picked by the scheduler
A process can become blocked for many reasons
- e.g. waiting for I/O, until an I/O interrupt signals to reschedule the process



## Process Control Block
The OS maintains information about a process in the data structure "Process control block" (PCB)

A process table is a list of PCBs, one for each process

Example info stored:
- Process ID, process state, parent process, memory management info, file descriptors, priority, used CPU time, etc.


# Threads

Threads provide an execution context to a process
- Sequential execution of a set of instructions
- Has a program counter, stack pointer, registers, stack

To run, the execution context is loaded into the CPU's registers

While not running, the context of the thread resides in main memory
- Registers are used for another thread.


Threads execute within the environment defined by a process
- A process has one or more threads
- Calling main entrypoint implicitly creates the main thread


**Address Space of Threads**

- All threads of a process share the same address space
- Code, data, and heap memory are shared between threads
- Each thread has its own stack

## Why Threads?
Parallelism is allowed because threads are processor-agnostic

Enable overlap of I/O with other activities
- Avoid blocking progress while waiting for I/O operations
- One thread waits for I/O while another thread does something useful with the CPU


## Thread Control Blocks (TCB)
Information stored in TCBs includes:
- Thread ID
- Stack Pointer
- Program Counter
- Other register values
- State (running, blocked, ready)
- Pointer to PCB of the process to which the thread belongs to

