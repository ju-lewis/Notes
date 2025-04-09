# Tutorial Questions
## Q1. Roles of the OS
An operating system functions both as an abstraction layer for userspace programs and a hardware resource manager for all processes (time/space multiplexing)

## Q2. Computer Components
*Disk:* non-volatile storage
*Memory:* volatile storage
*CPU:* Main processor
*ALU:* Sub-system of the processor, performs arithmetic operations

## Q3. Fetch-Decode-Execute Cycle
This cycle is used by the processor, running on a clock signal, to execute the instructions contained in a program. Instructions are fetched using the pointer stored in the program counter. They're then decoded in the instruction decoder to work out what the processor needs to do. These decoded instructions are then executed

## Q4. Register Categories
 General purpose
 Special purpose

## Q5. Types of Multiplexing
*CPU:* Time
*Memory:* Space
*Disk:* Space
*Network Card:* Time
*Printer:* Time



# Exercises
1. 360
2. `cat subjects | grep -Po "([A-Z]{4})(?=.*)"`
3. `cat subjects | grep -P "10001" | wc -l` => 8 total
4. `cat subjects | grep -Po "^C([A-Z]{3})(?=.*)" | uniq | wc -l` => 8 total
5. `cat subjects | grep -Po "(?<=COMP[0-9]{5} )(.*)" | sort -r` => models of computation
6. `cat subjects | grep -Po "(\w)(?=\w{3}\d{5}.*)" | sort | uniq | wc -l` => 15
7. `cat subjects | grep -Po "(\w{4})(?=\d{5})" | sort | uniq -c | sort -g` => MAST (40 occurrences)