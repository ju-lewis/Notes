

# Need for CPU Scheduling
Only one thread can execute at a time on a single-core processor, so multiprogramming requires the CPU to switch between threads (possibly belonging to different processes)

The *scheduling policy/algorithm* is responsible for this computation switching.

## Process vs. Thread Scheduling
The scheduling unit can be a (single-threaded) process or a thread

>[!note]
>In this course, we'll focus on single-threaded processes


## Context Switch
When the OS transitions between executing different threads/processes

A **thread context switch** (between threads of the same process) involves:
- Saving the execution context of the current thread to the TCB
- Loading the context of *another* thread from its TCB into the CPU

A **process context switch** involves:
- Saving/loading execution contexts
- Loading state related to memory management from the PCB (process control block)
- Flushing the *Translation Lookaside Buffer* (in a paged system with virtual memory)

There is much more overhead in a process context switch than a thread context switch

### Context Switch Control Flow
![[context-switch-diagram.png]]

Time spent in the OS performing the context switch is pure overhead.



### Process Behaviour
Most processes alternate bursts of computing with I/O requests (e.g. disk or network)

**CPU-Bound Process**:
- Spends most of the time performing computations (CPU burst) on the CPU
**I/O-Bound Process**
- Spends most of the time waiting for I/O



# CPU Scheduling


## Preemptive vs Non-preemptive Scheduling

**Non-Preemptive Scheduling**
- Pick a process to run and let it run until it block or voluntarily release the CPU

**Preemptive Scheduling**
Pick a process and:
- Let it run for a maximum for some fixed time (a quantum)
- If it's still running, suspend it and pick another process
Clock interrupts are needed to give control of the CPU back to the scheduler


>[!note]
>Preemptive context switching typically results in more context switching. Non-preemptive switching only switches when it's *absolutely necessary*


## Scheduling Environments
**Batch Systems**
- A set of (potentially periodic) jobs that need to run
- Jobs don't require interaction with user

We typically want non-preemptive scheduling or preemptive switching with a long quantum as interactivity is not required

**Interactive Systems**
- Interactive users expect fast response times
We want preemptive switching here


## Scheduling Goals
**Fairness**
- Processes get a fair share of the CPU
- Comparable processes should get comparable service
- *very hard to define*
- Starvation is a measure of fairness
**Efficient Use of Resources**
- Minimising context switching overhead


### System-Specific
**Batch Systems**
- Maximise throughput 
	- (number of processes that are completed per time unit)
- Minimise turnaround time 
	- (interval from the time of submission of a process to the time of completion, including time spent in the ready queue)
**Interactive Systems**
- Minimise response time 
	- (time between issuing a command and getting *a result*)
	- *Note:* response time $\neq$ completion time

# Non-Preemptive Scheduling Algorithms

## First-come First-served
Run processes in the order in which they become ready to execute
- FIFO queue
When the currently running process block/stops, the process that's been waiting the longest is selected

Processes get appended to the tail of the FIFO queue and dequeued from the front

### FCFS Analysis

**Benefits**
- Simple
- Easy to implement 
- Low context switching overhead
**Detriments**
- Convoy effect
	- Short processes (short CPU bursts) waiting behind long CPU-bound process
	- I/O bound processes
		- Might spend a lot of time queuing up
		- Reduced resource utilisation (e.g. I/O devices sit idle waiting for the process to get selected)
- Longer turnaround times
- Starvation is possible in an *entirely* CPU-bound process

## Shortest Job First
Schedule the job that has the least amount of work to do (shortest CPU burst) until its next I/O request or completion

Assume all processes became *ready* at time 0
- Turnaround time = time of completion - time of arrival


### SJF Analysis
**Benefits**
- Simple
- Easy to implement
- Optimal average turnaround time (for a given set of *jobs* that are available simultaneously)
**Detriments**
- Requires estimating the length of CPU burst s
- Processes with long CPU bursts can be starved


# Preemptive Scheduling Algorithms

## Round Robin
Run a process for a quantum, then switch to the next job in the *ready* queue
- Repeat until all processes are finished

Response time = time of first run - arrival time (to the ready queue)

### RR Analysis

Length of quantum in RR
- Long(er)
- The length of the quantum presents a trade-off
	- Making it long enough to amortise the cost of context switching without making it so long the system is no longer responsive

If quantum is *too* long, it morphs into FCFS
- Less context switching overheads

**Benefits**
- Simple
- Easy to implement
- Starvation is impossible
**Detriments**
- Very long turnaround times (but it maximises response times)

Unfair, as it favours CPU-bound processes over I/O-bound ones
- I/O bound processes are unlikely to use the whole quantum, so they have to wait at the back of the queue more






