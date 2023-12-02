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
executor.execute( runnableTaskInstance );
```
Simple example of copying content of multiple files to other files
```
public class Main {
 
    public static void main(String[] args) throws IOException {
		
	String sourceFile1 = "a.txt";
	String sourceFile2 = "b.txt";
		
	String destFile1 = "c.txt";
	String destFile2 = "d.txt";
		
	// Creates a fixed thread pool of size 5.
		
	ExecutorService executor = Executors.newFixedThreadPool(5);
		
	// Assume you are submitting 100 copy tasks,
	// then executor service uses a fixed thread 
	// pool of size 5 to execute them.
 
        executor.execute(new CopyTask(sourceFile1, destFile1));
	executor.execute(new CopyTask(sourceFile2, destFile2));	
    }
}
```

### Thread class methods
1. stop() - stop method is used to stop the execution of thread. but it leaves the system in incosistent state because we are not giving chance to rollback or revert the actions. DUe to this it is deprecated.
   
2. interrupt() - With this method, thread can decide wether they want to interrupt the task. When thread is alive this method return true.
   
3. interrupted() - this method is used to check the state of thread wether it is interrupted or not. When thread is alive this method return true.
   
4. sleep() - this method is used to BLOCK the thread for given interval of time. This method throws InterruptedException if the thread is interrupted while it is in sleep.

5. yield() -  This method instructs the thread schedular to pass the CPU to other waiting thread if any


### States of Thread
1. NEW - Thread is created but not yet started

2. RUNNABLE - thread is executing in JVM. Internally it has two sub-states : READY and RUNNING. when you start the thread it comes to Ready state and wait for the CPU, and if CPU is allocated then it goes into Running state. in other words when the Thread schedular suspends the thread then it goes back to the Ready state and waits for its turn again.

3. BLOCKED - thread is blocked if its waiting for Aquaring monitor lock. Synchronized block or method can be good example of it.

4. WAITING - Thread can be in waiting state for another thread to complete its task. wait and join methods

5. TIMED WAITING - Thread can be in waiting state for another thread to complete its task for given interva. wait(milis) or join(milis) methods used for this.

6. TERMINATED - Threads go to this state either by completing the task or in middle it got terminated.

### Thread Priorities
1. MIN_PRIORITY - 1 being the minimum priority
2. NORM_PRIORITY - 5 is the normally priority, this is the default priority value.
3. MAX_PRIORITY - 10 being the max priority.
   
```
Thread.setPriority(int newPriority)
```




