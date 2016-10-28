# Sec 9: Multithreading Questions

###1) What is multithreading?
Multithreading is a process of executing multiple threads simultaneously. Its main **advantage** is:  
-Threads share the same address space.  
-Thread is lightweight.  
-Cost of communication between process is low.  

###2) What is thread?
A thread is a lightweight subprocess.It is a separate path of execution.It is called separate path of execution because each thread runs in a separate stack frame.

###3)What is the difference between preemptive scheduling and time slicing?
Under **preemptive scheduling**, the highest priority task executes until it enters the waiting or dead states or a higher priority task comes into existence.   
Under **time slicing**, a task executes for a predefined slice of time and then reenters the pool of ready tasks. The scheduler then determines which task should execute next, based on priority and other factors.

###4) What does join() method?
The join() method waits for a thread to die. In other words, it causes the currently running threads to stop executing until the thread it joins with completes its task.


###5) What is difference between wait() and sleep() method?
![](sec2_31.png)






































