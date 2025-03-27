
# Preemptive Scheduling Continued

## Priority Scheduling
Assign a priority to each job, allocated the CPU to the highest priority process that is *ready* to run

- Priorities can be assigned:
	- Statically, at process creation
	- Dynamically, adjusted throughout the execution of a process


To avoid starvation:
- Change the priority of the running process with time, e.g. decrease priority after each clock interrupt (clock tick)
- Preempt process if its priority dropped below that of the next highest priority

### Multi-Level Feedback Queue (MLFQ)
Multiple queues, each with different priority
- The quanta processes are allowed to run for *increases* as the priority of the queue decreases

>[!note]
>Think about it like a stack of queues


Low priority -> large quantum
High priority -> runs often, small quantum

Processes start at the highest priority queue
- Used their quanta? Move to a lower priority queue
- Haven't used all their quanta (e.g. I/O-bound) Stay int he current priority queue

Processes in the queue with the highest priority get to run

The algorithm used to schedule processes within the same group is a parameter to the algorithm - e.g. *RR*

We don't want I/O bound processes sitting in queues behind long CPU burst processes!

**Note**: Starvation *is* possible if processes sink the lowest priority and new processes continue coming in.
- We can fix this by bumping low priority processes occasionally


One large benefit of MLFQ is that no a priori knowledge about processes is required


# Memory Management

**Why learn about memory management**?

Plays a key role in multi-programming
- To improve CPU utilization, multiple processes need to be loaded into memory

Security
- Isolation between processes and OS memory

Enable a computer system to run more processes with larger memory requirements
- A single process can use more memory than what is physically available

## Early Systems - No Memory Abstraction

Programs referenced physical memory directly

**Example**:
- `MOV AX, 1000` - moving the contents at physical address `1000` to `AX`

How can we achieve multi-programming under this model?
- Have the running process in memory and all other processes on disk
- On a context switch, the running process is swapped to disk and the newly scheduled process is swapped into memory

Issue:
- Consider 2 programs loaded into memory (in consecutive contiguous blocks) any `jmp` instructions in the second program may lead the program counter to enter the first program's memory addresses, since there is global memory addressing.


# Memory Abstraction

Provide a logical address space that is bound to a separate physical address space.
- Program instructions refer to *logical addresses*
- The OS manages physical memory
- The hardware translates logical addresses to physical addresses at runtime


**Two main approaches**
- Base and limit registers
- Paged virtual memory



## Base and Limit Registers
A program is loaded into consecutive memory addresses wherever there is room

Two registers in the CPU are used to delimit the physical memory location of the process
- **Base register**: contains the physical address where the program begins in physical memory
- **Limit register**: contains the length of the program

The values of the registers are determined by the OS and maintained in the PCB. They are loaded into the CPU when the process is running



Every time a process references memory, the CPU hardware:
- Checks that the logical address is *less than* the value of the limit register, if it is not, the memory is out of bounds and an exception (interrupt) is raised.
- If the logical address is within the bounds, the hardware add the base value to the logical address to obtain the physical address

Requires contiguous memory allocation

OS needs to manage physical memory by:
- Keeping track of memory usage
- Allocating free (contiguous) memory to processes
- De-allocating memory when a process is swapped to a disk or terminates

### Keeping Track of Memory Usage

One approach is to use a *linked list*

Each entry in the list specifies:
- A hole (H) or a process (P)
	- Free or busy?
- The address at which it starts
- The length of the hole or the allocation
- A pointer to the next entry


### Allocating Contiguous Memory
Choosing a free block of memory to allocate to a process

Once a free block is chosen, it is divided into 2 pieces:
- One for the process
- One for the unused memory
(Except in the statistically unlikely event of an exact fit)

#### Algorithms


**First-fit**
Selects the first free block that fits the process

- Fast, it searches as little as possible

**Best-fit**
Traverse the entire list, looking for the smallest block to which the process can be allocated

- Slowest than first-fit
- Tens to create small, useless free blocks because it produces the smallest leftover memory hole

**Worst-fit**
Allocate the process to the largest available free block
- Produces the largest leftover memory holes

### De-allocating Contiguous Memory
Required when a process terminates or is swapped out of memory

Swapping
- When not running, a process can be swapped to disk and then brought back into memory when it resumes execution
- Makes it possible for the total physical address space of all processes to exceed the real physical memory of the system

The data structure representing the state of physical memory must be updated accordingly


### External Fragmentation
As processes are loaded and removed from memory, free memory might be broken into small pieces
- *in total* there is enough space for a process
- *in reality* we can't fit the new process in contiguous space



### Limitations of Base and Limit Registers

- An entire process must be loaded into contiguous memory addreses
- A process cannot be larger than physical memory
- When more space is needed, the entire process needs to be swapped to disk
- External fragmentation


## Paged Virtual Memory
Break up the address space of a process into fixed-sized piece called *pages*

Break up physical memory into fixed-sized slots called page *frames*

>[!note]
>Pages -> logical
>Frames -> physical

Pages are mapped to frames
- Pages and frames are generally the same size
- Pages don't need to be stored in contiguous frames

Not all pages have to be in physical memory at the same time to run a process
- During the lifetime of a process, pages start out on disk and may move between disk and memory any number of times
- When a page is moved to disk and back again, it may be put ion a different page frame than before


The operating system maintains a *page table* which records the mappings from pages to frames
- Each entry indicates where each page is placed in physical memory

The *Page Table Base Register (PTBR)* points to the start of the page table

