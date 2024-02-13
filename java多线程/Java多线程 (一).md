https://www.youtube.com/watch?v=TBcCWgZcY6U     

Process: Processes are basically the programs that are dispatched from the ready state and are scheduled in the
CPU for execution. PCB (Process Control Block) holds the concept of process. A process can create other processes which are known as Child Processes. The process takes more time to terminate and it is isolated means it does not share the memory with any other process.      
The process can have the following states new, ready, running, waiting, terminated, and suspended.     

Thread: Thread is the segment of a process which means a process can have multiple threads and these multiple threads are contained within a process. A thread has three states: Running, Ready, and Blocked.
The thread takes less time to terminate as compared to the process but unlike the process, threads do not isolate.  
PCB Process Control Block     
While creating a process the operating system performs several operations.     
To identify the processes, it assigns a process identification number (PID) to each process. As the operating system supports multi-programming, it needs to keep track of all the processes. For this task, the process control block (PCB) is used to track the process's execution status. Each block of memory contains information about the process state, program counter, stack pointer, status of opened files, scheduling algorithms, etc. All this information is required and must be saved when the process is switched from one state to another. When the process makes a transition from one state to another, the operating system must update information in the process's PCB. A process control block (PCB) contains information about the process, i.e. registers, quantum, priority, etc. The process table is an array of PCBs, that means logically contains a PCB for all of the current processes in the system.       

为什么要线程？     
• Threads run in parallel improving the application performance. Each such thread has its own CPU state and stack, but they share the address space of the process and the environment!        
• Threads can share common data so they do not need to use interprocess communication. Like the processes, threads also have states like ready, executing, blocked, etc.      
• Priority can be assigned to the threads just like the process, and the highest priority thread is scheduled first.              
• Each thread has its own Thread Control Block (TCB). Like the process, a context switch occurs for the thread, and register contents are saved in (TCB). As threads share the same address space and resources, synchronization is also required for the various activities of the thread.   

为什么要多线程？    
A thread is also known as a lightweight process. The idea is to achieve parallelism by dividing a process into multiple threads. For example, in a browser, multiple tabs can be different threads. MS Word uses multiple threads: one thread to format the text, another thread to process inputs, etc. More advantages of multithreading are discussed below.       
Multithreading is a technique used in operating systems to improve the performance and responsiveness of computer systems. Multithreading allows multiple threads (i.e., lightweight processes) to share the same resources of a single process, such as the CPU, memory, and I/O devices.   


Threads can be created by using two mechanisms:    
1. Extending the Thread class   
2. Implementing the Runnable Interface

![截屏2024-02-13 13.31.27.png](https://img.xwyue.com/i/2024/02/13/65cb6f35dd028.png)

race conditions: the program ends with an undesired output, resulting from the sequence of execution among the processes.    
deadlocks: the concurrent processes wait for some necessary resources from each other. As a result, none of them can make progress.      
resource starvation: a process is perpetually denied necessary resources to progress its works.      

![截屏2024-02-13 13.37.47.png](https://img.xwyue.com/i/2024/02/13/65cb70b414ae1.png)


