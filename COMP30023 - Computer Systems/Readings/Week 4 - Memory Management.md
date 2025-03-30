

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


# Paged Virtual Memory

