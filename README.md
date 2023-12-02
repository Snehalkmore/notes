# Notes of Multithreading

### Thread defination-
Thread is lightweight process which has its own context and stack to preserve the state of it. 

### Thread creation approaches :
1. extending Thread class
2. Implementing the Runnable interface

### methods invoked :
1. run - 
     run method is the entry point to start the execution of thread.
2. start - 
    execution of thread should be initiated with this method. Thread is in ready started but not yet running. It marks thread as in ready state and waits for CPU to be allocated.


## ExecutorService
why executorService introduced? 
- to perform different task parellely, required creating multiple thread. To create thread is COSTLY process because it requires to create seperate context and stack for each thread. Instead of creating thread for each task, we can create the pool of threads which is possible with 'ExecutorService'. 

How executorService works? 
- If any task is created and if thread is available in threadPool, then task is assigned to the thread. Otherwise it will go to blocking queue and kept there till thread is available.

What is way to create thread/threads using executorService ?
```
ExecutorService executor = Executors.newFixedThreadPool(5);
```

