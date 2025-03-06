
An OS is a program that interfaces the machine with the application programs
- Its main job is managing resources efficiently for userspace programs

**Key functionality**
- Provides hardware abstraction
- Manages hardware resources


# Hardware Abstraction

>[!info] Goals
>- Present a simpler, cleaner, easy to use and understand model of the computer
>- Present an application with a simpler abstract machine that appears to be dedicated to itself

## Abstraction examples
The primary *processor* abstraction are *threads*
- Implicit thread creation on program execution
The primary *memory* abstraction is an *address space*
- Allocating reserved areas for programs to use in memory, preventing overwriting and permitting virtual memory
The primary *disk/non-volatile memory* abstractions are *files*
The primary *network interface* abstractions are *sockets*

Processes encompass all of these abstractions.

---
# Resource Management

Operating systems utilise both *time* and *space* multiplexing
- Time -> time sharing
- Space -> memory/address space allocation



# Computer Architecture

## Processor structure
**Registers**
- Located on the processor die
- Extremely fast
- Both general purpose and special purpose
**Arithmetic Logic Unit**
- Performs bitwise addition/subtraction/multiplication*/division*
**Memory Management Unit**
- Provides a data/addressing interface to the memory

### Other stuff :D  (Some are optional)
**Instruction Decode Unit**
- Parses opcodes/targets from instructions
**Memory Cache**
- On-die volatile memory for fast access (tiered as L1, L2, L3)
**Branch predictor**
- Pre-caches commonly used addresses based on execution patterns
**Floating Point Unit**
- Hardware acceleration for floating point operations
**SIMD Vector Processing Unit**
- Permits single-instruction manipulation of large amounts of data
**Compute Units**
- Highly parallelised processing unit for graphical/texture/matrix applications

---

# Process Internals

## Calling Subroutines
Callee is responsible for maintaining stack/specific registers based on the calling convention

Caller is responsible for configuring the stack and registers for the callee based on calling convention


