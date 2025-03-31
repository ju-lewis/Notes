

# No Memory Abstraction
Early mainframe computers had no memory abstraction
- Every program sees the physical memory

Under these conditions, it was *not possible* to have more than 1 program running in memory at the same time.

3 different memory configurations arose for positioning OS-related software:

1. Place the OS at the bottom of RAM
2. Place the OS in ROM (at the top of memory)
3. Place device drivers in ROM and the OS in RAM

Concurrent execution had to be achieved using memory swapping
- Storing execution context in non-volatile storage


# Address Spaces

Address spaces are the set of addresses exposed to the process.
- They map to different physical addresses, but the process doesn't need to know this.

## Base and Limit Registers

**Base register**: stores the start of the address space
**Limit register**: stores the length of the address space

Lookup:
- Check the address is smaller than the limit register
- Add the address to the base register to resolve the physical address


## Swapping

Saving/loading execution contexts from disk


## Memory Management with Bitmaps


## Memory Management with Linked Lists

You can store a linked list between holes / occupied regions
- Each region stores a base/limit pointer


# Paged Virtual Memory

Each program has its own address space, which is broken up into chunks called *pages*
Pages are mapped onto physical memory

Not all pages have to be in physical memory at the same time to run the program!


## Paging

Program-generated addresses are called *virtual addresses* and form the *virtual address space*

Physical memory is divided into *frames*.


Typically there are more pages than frames in a system.

Modern operating systems often support mixed size pages:
	e.g. 4KB for user applications and 1GB for the kernel


Page faults occur when a program references an address in a page that doesn't currently occupy a frame.
- Present/Absent bit = 0 in page table entry


### Page Tables

A common size for a page table entry is 32 bits

Entries often contain:
- Page frame number
- Present/absent bit
- Protection bit (read/write access locks)
- Modified bit
- Referenced bit

### Translation Lookaside Buffer

Hardware cache supporting much faster address resolution

### Page Replacement

When a page fault occurs, the OS has to choose a page to evict to make room for the new page.

If the page has been modified while in memory, it must be rewritten to the disk to bring the disk copy up to date
- If it hasn't no rewrite is needed.


See specific page replacement algorithms [[L8 - Virtual Paged Memory Continued#Page Replacement Algorithms|here]].
- Generally the premise is to store a data structure of tables (either an order preserving one like a linked list for FIFO related algorithms) or a table using a set of counter bits for a LRU implementation




