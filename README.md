# Process Management Application with Strategy and Observer Design Pattern

You should
fulfill the concepts of:

```
 Strategy Design Pattern
 Observer Design Pattern
```
In this application, there will be processes which has the following attributes:

- id
- arrival time that is the time at which the process arrives in the ready queue
- burst time that is the time required by a process for CPU execution
- completion time which is arrival time plus burst time
- waiting time
- priority
- process state
Arrival time and burst time will be random integers which are between 1 and 20. Priority will be a
random integer between 1 and 10, 1 will be the highest priority.

Process states are **_New_** , **_Ready_** , **_Running_** , **_Blocked_** , **_Terminated_** and **_Starved._**

In this application processes will be scheduled by using following scheduling algorithms:

- **First Come First Serve** that schedules according to arrival times of processes.
- **Shortest Job First** that schedules according to the shortest burst time.
- **Priority** that schedules according to the priority.

Imagine that this is a multiprogramming environment, therefore scheduling is putting processes in an
order to be executed sequentially in CPU, there are no parallel processes. One single CPU executes
processes one after the other. Do not try to follow real world operating system rules, only follow the
rules defined here.

Also, there is an observer for each process state e.g. ReadyStateObserver, NewStateObserver. These
will update process state when they are notified.

There will also be a **ProcessBatch** class which has a batch of processes and is responsible of:

- Scheduling processes in the batch
- Determining each process’ waiting time.
- Waiting time will be determined after scheduling and according to burst times. For example,
    P1 with burst time 3, P2 with burst time 7, P3 with burst time 4 are scheduled in the given
    order.

P1 will have waiting time 0 since it is the first one. P2 will have waiting time 3 and P3 will have 10. If a
process has waiting time more than 50, then its state must be notified as **_Starved_**.

- Each time a new process is added to the batch, its state must be notified as **_New_**.


- When the waiting time of a process is determined in batch, its state must be notified as **_Ready,_**
    unless it is in starvation.

A **Dispatcher** class will extract the scheduled processes which are in ready queue. These processes’
states must be updated as **_Running_** and will be sent to the **CPU** class. After CPU runs the process, the
process’ state will be **_Terminated_**.

If the state of the process in ready queue is set as starved after determining the waiting time, it will
be **_Blocked_**.
