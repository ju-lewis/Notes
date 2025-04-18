
# Subroutines
## Calling
- Register values are stored in the stack at the location pointed to by SP
- The return address is stored in the stack (below the subroutine stack frame)
- The PC is loaded with the address of the entry point of the subroutine
- The stack pointer is updated to point to the new top of the stack

## Returning
- Register values and stack must be restored
- PC is loaded with the return address (found on the stack)


# Memory Boundaries
HW support to enforce memory boundaries between processes
- Allows the operating system to prevent one application from modifying the memory of itself and other programs

# Execution Mode
The *mode bit/flag* in the program status word (PSW) indicates the execution mode of the process
- Kernel mode/user mode

**User Mode**:
- Cannot issue privileged instructions
- Can only access specific sections of memory allocated to the program
**Kernel Mode**:
- Can issue all instructions
- Can access all memory

Privileged instructions are instructions that affect control of the machine or do I/O
- This is why syscalls exist (kernel functions)


# Basic Operation of an OS
Not all instructions from a user-space program are required to be processed by the OS, non-privileged instructions can be directly executed by the CPU
- OS is interrupt driven


![[os-diagram.png]]

## Interrupts
- Events that cause the CPU to *not* execute the next instruction
- CPU enters kernel mode and executes an OS interrupt handler
- The interrupt vector points to the corresponding ISR

### Types of Interrupts
- External interrupts - generated by external devices at unpredictable times
	- Clock interrupts
	- I/O device interrupts
- Internal interrupts - caused by an exception when executing the current instruction
	- Error condition
	- A temporary problem


## System Calls
Interface between user programs and OS

System call execution:
1. Put the system call number in a place where OS expects (typically accumulator)
2. Execute a TRAP instruction to switch from user mode to kernel mode and start execution at a fixed address within the kernel
3. The kernel code that starts following the TRAP examines the system-call number and dispatches the corresponding handler


# Why Processes?
Support the ability to run multiple programs concurrently on a single CPU


