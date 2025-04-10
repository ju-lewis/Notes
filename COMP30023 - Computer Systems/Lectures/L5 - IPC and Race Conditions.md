
# Interprocess Communication (IPC)
Processes frequently need to share resources/data with other processes

**Issues:**
- How? - Shared memory, pipes, files, sockets, signals
- Cooperating processes may interfere with each other and require an orderly execution

**Our focus**: understanding and avoiding race conditions in cooperating processes

>[!note]
>In these lecture notes, process and thread are used interchangeably because the same problems and solutions apply to both in this context.

## Race Conditions
Occur when multiple processes/threads access a shared resource
- Result depends on timing of code's execution
- Results are indeterminate

>[!example]
>Consider a scenario where the is a global variable: `Stack s;` 
>*two* threads execute a code block that:
>1. Checks if the stack is empty
>2. If not, it pops an element from the stack

A race condition can lead to undefined results if both threads read the stack as non-empty (due to CPU time-sharing) and attempt to pop from the stack
- Could lead to crash, seg-fault, etc.

### Avoiding Race Conditions
**Critical Regions**: part of the program where the shared resources are accessed
**Mutual Exclusion**: Guarantee that only 1 process/thread executes within the critical region at any given point in time


If the previous example had a form of mutual exclusion, the situation where both threads read the stack as non-empty could never happen, as the first thread/process entering the critical region (by reading the stack) would cause the second thread/process to block until the first thread/process leaves the critical region.

# Mutual Exclusion

>[!note] Conditions for Mutual Exclusion
> General idea: use locks to control access to the critical region.
> 
> *Acquire lock* to enter the critical region
> *Release lock* when exiting the critical region
> Only the process/thread with the lock can be in the critical region


## Lock Variables
A possible implementation using locks would be to have a global lock variable
- Threads busy wait until the lock variable becomes `0`
- When this happens they set the lock to 1 and execute critical region
- After executing critical region unset the lock variable
**However**, this has the same issue where 2 threads can read the lock as unset if the processor context-switches immediately after thread A reads the lock, causing both threads to execute the critical region at the same time.

A solution to this could be *continuously* checking the lock variable while executing the critical region

## Busy Waiting

**Cons**:
- Waste of CPU
- Priority Inversion Problem

### Priority Inversion Problem
Consider a computer with 2 running processes
- $P_{high}$ - high priority
- $P_{low}$ - low priority

Scheduling rules: $P_{high}$ always gets to run as long as its not *blocked*

At a particular moment:
- $P_{low}$ is in the critical region
- $P_{high}$ becomes ready to run (e.g. I/O operation completes)
- Current quantum ends ($P_{low}$ stops running)
- $P_{high}$ starts running and begins busy waiting (can't enter critical period because $P_{low}$ is in it.)
- $P_{low}$ can never exit the critical region because it never gets scheduled to use the CPU while $P_{high}$ is running
- $P_{high}$ loops forever

### Strict Alternation
A busy waiting approach in which 2 processes/threads take turns running the critical region

>[!example]
>We can implement this using an alternating lock variable
>
>```c
>int turn;
>
>void threadA() {
>	while (1) {
>		while (turn != 0){}
>		criticalRegionA();
>		turn = 1;
>	}
>}
>
>void threadB() {
>	while (1) {
>		while (turn != 1){}
>		criticalRegionB();
>		turn = 0;
>	}
>}
>```

This works because the threads have different critical region entry conditions, so by design there is no way both threads can simultaneous enter the critical region, regardless of time-multiplexing/context-switching

### Test and Set Lock (TSL)
TSL is an assembly mnemonic representing and instruction for *hardware* register locking

`TSL REGISTER, LOCK`
1. Copy contents of `LOCK` into `REGISTER`
2. Store non-zero value in `LOCK`

TSL's operations are *atomic*
Atomic operations are indivisible, all or nothing.

This is important, because there *CANNOT* be a context switch between testing the lock's value and setting it.
- This means we can't have multiple threads reading the lock as unset and entering the critical region.

### Mutex Using TSL and Busy Waiting
**To enter critical region:**
1. `TSL REGISTER, LOCK`
2. if `REGISTER` is 0, enter critical region
3. is `REGISTER` is *not* 0, lock is set so go back to step 1 (busy wait)
**When leaving the critical region**:
4. Set lock to 0

```asm
enter_region:
	TSL REGISTER, LOCK
	CO
```

## Blocking

General approach:
When a thread wants to enter its critical region
- It checks if entry is allowed
- If not, let another thread use the CPU while waiting for the lock
- How? - block, yield, etc.

**Cons**:
- Approach-specific (e.g. starvation, overhead of system calls, overhead of context switches)

### Yield Mutex

Hardware support for the process/thread to voluntarily yield access to the CPU.

```asm
mutex_lock:
	TSL REGISTER, MUTEX ; Copy value of mutex and set mutex to 1 (atomic)
	CMP REGISTER, #0    ; See if the mutex was unlocked
	JZE ok              ; If it was unlocked at test, jump to `ok`
	CALL thread_yield   ; If it wasn't unlocked, yield CPU
	JMP mutex_lock      ; Check lock status again
ok:	RET                 ; Return if unlocked (enter critical region)

mutex_unlock:
	MOV MUTEX, #0       ; Set the MUTEX to be unlocked
	RET
```


>[!Note]
>This approach *can* cause excessive context switching with round-robin-like scheduling algorithms if multiple processes/threads are waiting for a single critical region. (Each thread/process will continuously be scheduled just to poll the lock and return to the ready queue when they yield control)




