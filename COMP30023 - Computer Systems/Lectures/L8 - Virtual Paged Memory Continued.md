
# Paging
Pages (logical memory) appear as contiguous memory to a user program, but are mapped to non-contiguous frames in the physical memory through a page table.


**Transforming Logical Addresses to Physical Addresses** (by hand)

1. Determine the *page* the logical address resides in
2. Look for the frame entry corresponding to the *page* within the page table
3. Multiply the frame number by the page width (in bytes) to get the *base* of the frame in the physical memory
4. Add the *offset* of the address within the page to the frame base address to get the final physical address.


## Structure of a Logical Address
**Logical Address**
- The first $m-n$ bits represent the page number
- The last $n$ bits represent the page offset

$m$ bits to represent the logical address
- Size of the logical address space is $2^m$

$n$ bits to represent the page offset
- The page size is $2^n$

$m-n$ bits to represent the page number

This allows the CPU to efficiently lookup the frame number and add the offset, as they're separate numbers
- No multiplication is required because we can directly store the frame address, instead of the frame *number*

## Internal Fragmentation

When a process is divided into fixed-size pages, there may be some leftover space of the *last page*
- Process memory requirements are *rarely* multiples of the page size

**Effects of Page Size**
Large pages:
- More internal fragmentation
- Smaller page tables
Small pages:
- Large page tables

## Structure of a Page Table Entry
Aside from the frame number, a page table entry contains other useful information about the page. For this subject we're interested in:
- Present/absent bit
	- Indicates whether the page is in physical memory (1) or on disk (0)
	- If 0, the MMU will *not* translate the address and will trigger a page fault interrupt
- Referenced bit
	- When a page is referenced, the MMU automatically sets the referenced bit to 1
- Modified bit
	- When a write occurs on the page, the MMU sets the modified bit to 1

### Page Fault
Some pages of a process may not be mapped to frames

If a process references an address of a page not currently mapped to a frame, the MMU raises a page fault through an internal interrupt

On a page fault, the OS:
- If there are *no free frames*, picks a page frame to evict and writes its contents to disk
	- Only saves it if the modified bit is set
- Fetches the page that was referenced (from disk) and loads it into the page frame that was just freed
- Updates the page table
- Restarts the process at the instruction that caused the page fault


## Page Replacement Algorithms
How to pick a page frame to evict when a page fault occurs?

Page replacement algorithms:
- Optimal
	- Leads to the fewest number of page faults overall
	- Evict the page that will be accessed furthest in the future
	- Useful as a comparison point, but not practical
- First-in, first-out
- Second-chance
- Least Recently Used (LRU)

### First-in, First-out (FIFO)
Evict the page that has been in memory the longest
Maintain a FIFO queue of pages based on load time
- Page loaded the longest ago is at the head
- Most recently loaded page is placed at the tail


>[!note] Principle of Locality
Most programs exhibit temporal and spatial locality
>
>**Temporal Locality**
>- If a process accesses a particular memory address, it will likely reference it again in the near future
>  
>**Spatial Locality**
>- If a process accesses a particular memory address, it will likely reference nearby addresses in the near future
>

### Second-Chance Algorithm
Simple modification to FIFO to avoid evicting a recently used page

Inspect the referenced bit of the oldest page
- If the bit is 0, it has not been used recently, evict
- If the bit is 1
	- Clear the R bit
	- Move the page to the tail of the queue (give it a second chance)
	- Update the load time of the page as if it had just arrived in memory


### Least Recently Used (LRU)
Pages that have been accessed in the near past are likely to be accessed again in the near future

Evict the last-recently-used page

Possible implementation:
- Maintain a list of all pages with the most recently used page at the head and the least recently used at the tail
- The page at the tail is chosen for eviction
- On every memory reference, move the referenced page to the head

Approximates the optimal algorithm

Theoretically possible, but has massive overhead on memory acceses

### LRU Approximation - Aging
Maintain a *bit counter* for each page

At each clock interrupt (tick):
- Shift all counters by one bit to the right
- Append the *referenced bit* to the leftmost bit

Evict the page with the lowest counter

**Limitations**
- Aging may evict a page that was not the least recently used


## Translation Lookaside Buffer (TLB)

Without optimisation, in a paged system, each memory references requires 2 memory access: one to access the page table and one to access the data

The TLB is a hardware cache in the MMU

Stores copies of recently accessed *page table entries*
Implemented using associative circuitry (hardware parallelism)


>[!note] Lookup Process
>
>1. Take the page number from the logical address
>2. Perform TLB lookup
>- On TLB hit, we can go straight to the physical memory with the frame address 
>- On TLB miss, we have to lookup the frame address in the main memory page table
>3. Get the physical address from the frame address and the page offset

