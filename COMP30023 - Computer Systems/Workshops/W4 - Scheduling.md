
## Q5. Batch Job Scheduling
5 batch jobs arrive at the same time - (A,B,C,D,E)
They have estimated running times  - (10, 6, 2, 4, 8) in minutes
The have priorities                               - (3, 5, 2, 1, 4)

Determine average turnaround time for the following algorithms (ignoring switching overhead)

**a.** Round robin - quantum is 6 minutes (runs in order A,B,C,D,E,F)

A runs for 6 minutes (4 mins remaining)
B  runs for 6 minutes (completes)
C runs for 2 minutes (completes)
D runs for 4 minutes (completes)
E runs for 6 minutes (2 mins remaining)
A runs for 4 minutes (completes)
E runs for 2 minutes (completes)

*Turnaround times*:
- A - 28 mins
- B - 12 mins
- C - 14 mins
- D - 18 mins
- E - 30 mins

Average: 20.4 mins

**b.** Non-preemptive priority scheduling

B runs for 6   mins (completes)
E runs for 8   mins (completes)
A runs for 10 mins (completes)
C runs for 2   mins (completes)
D runs for 4   mins (completes)

*Turnaround times*:
- A - 24 mins
- B - 6 mins
- C - 26 mins
- D - 30 mins
- E - 14 mins

Average: 20 mins

**c.** FCFS, in order (A,B,C,D,E)

A runs for 10 mins
B runs for 6 mins
C runs for 2 mins
D runs for 4 mins
E runs for 8 mins

*Turnaround times*:
- A - 10 mins
- B - 16 mins
- C - 18 mins
- D - 22 mins
- E - 30 mins

Average: 19.2 mins

**d.** Shortest job first

C runs for 2 mins
D runs for 4 mins
B runs for 6 mins
E runs for 8 mins
A runs for 10 mins

*Turnaround times*:
- A - 30 mins
- B - 12 mins
- C - 2 mins
- D - 6 mins
- E - 14 mins

Average: 12.8 mins


# Workshop Questions

## 3.2

Failed assert is sent the signal `SIGABRT`


## 3.4.1
`kill PID`  results in status 143
`kill -SIGTERM PID`  results in status 143
^^ same!

`kill -SIGINT PID` results in status 130
ctrl-c quitting results in status 130
^^ same!


