
# Tutorial Questions
## Q1. Page Table Entries

**1a.**: $512$KB memory with a page size of $512$ bytes
Num. entries = $\frac{512 \times 1024}{512} = 1024$
Page table memory footprint = $1024 \times 4 = 4$KB

**1b.** $4$GB memory with a page size of $512$ bytes
Num. entries = $\frac{4 \times 1024 \times 1024 \times 1024}{512} = 8192\times1024$ 
Page table memory footprint = $8192 \times 1024 \times 4 = 32$MB

**1c.** 4GB memory with a page size of $512$ bytes
Num. entries = $\frac{4 \times 1024 \times 1024 \times 1024}{8 \times 1024} = 512 \times 1024$
Page table memory footprint = $512 \times 1024 \times 4 = 2$MB


## Q2. Translation Lookaside Buffer
Given the memory system:
- TLB can hold 1024 entries
- TLB lookup time = 1 cycle (1 nsec)
- PTE can be found in 100 clock cycles (100 nsec)
- Average page replacement time is 6 milliseconds

If page references are handled by the TLB 99% of the time, and only 0.01% lead to a page fault, what is the effect address translation time?

---

First, consider a TLB hit:
- Lookup time = 1 nsec

Now consider a TLB miss:
- 99.9% chance of taking 100 nsec for lookup 
- 0.01% chance for taking 6 milliseconds (page fault occurs)

Computing the weighted average:
$\text{Effective translation time} = (0.99\times1) + (0.0099\times100) + (0.0001\times6\times10^6) = 602$ 
Hence 602 cycles are required on average


## Q3. Address Sizes
Consider a logical address space of $64$ pages with $1024$ bytes, mapped onto a physical memory with $32$ frames.

**3a.** How many bits are there in the logical address?
- $64 = 2^6$ pages $\implies$ $6$ bits are required for indexing the page
- $1024 = 2^{10}$ bytes per page $\implies$ $10$ bits are required for indexing the offset

Hence $16$ bits are required for the logical addresses.


**3b.** How many bits are there in the physical addresses?
- $32 = 2^5$ frames $\implies$ $5$ bits required
- $1024=2^{10}$ bytes per page $\implies$ 10 bits are required

Hence $15$ bits are required for physical addresses.


## Q4. Page Table Entries
A machine has 48-bit virtual addresses and 32-bit physical addresses


**4a.** If pages are 4KB, how many entries are in the page table?

Remember, the page table has an entry for *all pages*. Because the pages are $4$KB = $2^{12}$ bytes each, we require $12$ bits to address within the pages. Hence the remaining bits in the virtual addresses are $48-12=36$ bits. This means we have $36$ bits for storing the *page numbers*, so we have $2^{36}$ entries. 



**4b.** 
The system has a 32 entry TLB
A program has:
- Instructions that fit in 1 page
- Sequentially reads elements from an array that spans thousands of pages

*How effective will the TLB be?*

As the array read begins, the program will eventually reference an address in a page *not* cached in the TLB. As a result, that page will be cached in the TLB. It depends on the size of the datatype, but if we assume we're reading *4 byte integers* then we'll have 1 lookup cache the page and $2^{10}-1$  subsequent lookups reference the cached page.

Hence, we get TLB misses every $2^{10}$ lookups



## Q5. Second-Chance Replacement

If all pages have their reference bits set to 1, they will all be given a "second chance", which involves setting their reference bits to 0 and placing them at the back of the queue.

After they all cycle back through the queue, they'll reach the front of the queue in the same order they were initially in (first-in-first-out)




