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
   
4. sleep() - this method is used to BLOCK the thread for given interval of time. This method throws InterruptedException if the thread is interrupted while it is in sleep. This method pauses the current thread and DOES NOT release any locks. This method belongs to thread call and called in any context by Thread.sleep(1000)

5. wait() - instance method that’s used for thread synchronization. it can only be called from a synchronized block. It releases the lock on the object so that another thread can jump in and acquire a lock. This method Releases the lock over the object and takes the thread to WAITING state. And the thread remains in that state until some other thread calls the notify() method over the same object.
   
6. yield() -  This method instructs the thread schedular to pass the CPU to other waiting thread if any

7. Thread.currentThread() - returns a reference to the current thread.

8. setDaemon(true) : we can set thread as daemon thread.

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

### Daemon thread
Daemon threads are the ones which does not prevent the JVM from exiting the application once it finishes. performing background tasks such as garbage collection or collecting application statistics etc. 
Note that the Java Virtual Machine exits when the only threads running are all daemon threads.
```
public class Main1 {
 
    public static void main(String[] args) {
		
	System.out.println("System threads..........");
		
	Thread thr = Thread.currentThread();
	ThreadGroup grp = thr.getThreadGroup();
	while (grp.getParent() != null) {
	    grp = grp.getParent();
	}
		
	Thread [] threads = new Thread[10];
	int n = grp.enumerate(threads);
		
	for (int i=0; i < n; i++) {
	    System.out.println(
		"Thread Name: " + threads[i].getName() + 
		" ; isDaemon: " + threads[i].isDaemon());
	}
    }
}
Output -
System threads..........
Thread Name: Reference Handler ; isDaemon: true
Thread Name: Finalizer ; isDaemon: true
Thread Name: Signal Dispatcher ; isDaemon: true
Thread Name: main ; isDaemon: false
```

### Callable interface
callable interface allows us to perform asynchronous task which is capable of returning result
```
interface Callable<V> {
    V call() throws Exception;
}
```
#### Future 
When you submit a Callable task to the ExecutorService, it returns a Future object. 
This object enables us to access the request and check for the result of the operation if it is completed.

Future has some important methods:
1. isDone() - Returns true if the task is done and false otherwise.

2. get() - Returns the result if the task is done, otherwise waits till the task is done and then it returns the result.

3. cancel(boolean mayInterrupt) - Used to stop the task, stops it immediately if not started, otherwise interrupts the task only if mayInterrupt is true.

```
import java.util.concurrent.Callable;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
 
class MyMath {
    public static int add(int a, int b) {
        return a + b;
    }
}
 
public class Main {
    
    public static void main(String[] args) throws Exception {
	
	int x = 10;
	int y = 20;
		
	ExecutorService executor = 
                Executors.newFixedThreadPool(1);
	
        // Submit a Callable task and use the Future
        // object to fetch the result.	
	Future<Integer> future = 
                    executor.submit(
		        new Callable<Integer>() {
			    public Integer call() {
			        return MyMath.add(x, y);
			    }
			});
 
	 // do some parallel task
	 // Inefficient to simply wait,
         // instead you can release the CPU 
         // by calling Thread.yield() inside 
         // the while loop.	

	while( ! future.isDone())
		; // wait
	
         // fetch the result 	
	 int z = future.get();
		
	 System.out.println( "Result is " + z );
    }
}
```

### Thread Syncronization
 Thread synchronization is used to solve concurrency problems that exist in parallel processing. Concurrency problem occurs when multiple threads are accessing the same SHARED OBJECT.
 example - 
 1. multiple transaction getting performed on same account
 2. multiple people trying to reserve ticket for same seat

Synchronization can be achieved:
1. synchronized method
2. synchronized block
3. locks

synchronized method
```
class Sample {
    synchronized void f() {...}
}
```

synchronized block
When synchronization is not required for the entire method i.e only certain part of the code must be synchronized then we use synchronized block.  
```
synchronized( object ) {
  // operations over the object
}
```
### Thread Safe Code or Re-entrant code
When code is safe from concurrency problem then it is called as re-entrant code.

### Deadlock
when two thread are trying to aquaire lock on object which are already aquired by oppsite thread, in that case deadlock occurs.

Issue with below code is writer1 aqaured lock on pen and writer2 aquired lock on book
```
class Writer1 extends Thread {
	
    Object book;
    Object pen;
	
    public Writer1(Object book, Object pen) {
	this.book = book;
	this.pen = pen;
    }
	
    @Override
    public void run() {
		
	synchronized(book) {
	    try { Thread.sleep(10); } catch(Exception e) {}
	    synchronized(pen) {
		System.out.println("Writer1 writing");
	    }
	}	
    }
}
 
class Writer2 extends Thread {
	
    Object book;
    Object pen;
	
    public Writer2(Object book, Object pen) {
	this.book = book;
	this.pen = pen;
    }
	
    @Override
    public void run() {
		
	synchronized(pen) {
	    try { Thread.sleep(10); } catch(Exception e) {}
	    synchronized(book) {
		System.out.println("Writer2 writing");
	    }
	}	
    }
}
 
public class Main {
 
    public static void main(String[] args) {	
	Object book = new Object();
	Object pen = new Object();
		
	new Writer1(book, pen).start();
	new Writer2(book, pen).start();
		
	System.out.println("Main is done");
    }
}
```
Solution : changing squeunce of lock in writer2
```
@Override
 public void run() {
    synchronized(book) {
        try { Thread.sleep(10); } catch(Exception e) {}
	synchronized(pen) {
	    System.out.println("Writer2 writing");
	}
    }	
 }

```

### Reentrant Locks
#### Read/Write Lock -
```
ReadWriteLock rw_lock = new ReentrantReadWriteLock();
 
```
Read/Write Lock gives us more flexibility during locking and unlocking. Based on the type of operation being performed over the object we can segregate the locks into

1) readLock - readLock allows us to lock the object for read operation, and the interesting point is that the read operation can be shared i.e if two threads are waiting for readLock then both of them can proceed forward with the operation as read operation doesn't change the data.

2) writeLock - writeLock is mutually exclusive i.e. if a writeLock is accepted then all the other lock requests should wait till the thread that owns the lock releases it.

example
```
T1 -> lock.readLock();

T2 -> lock.readLock();   ------  T1, T2, T3 can share the readLock and proceed forward with the operation

T3 -> lock.readLock(); 

T4 -> lock.writeLock();  -----T4 should wait till T1, T2 and T3 unlocks.

T5 -> lock.readLock(); -------t5 is in wait state since t4 is in wait state

```
This is in contrast to synchronized methods/blocks because for synchronized method/block there is no segregation of read and write operations. Object is locked no matter whether it is read or write.

```
Caution - It is always better to put the unlock operation in finally, as you need to unlock irrespective of exceptions.
```

example
```
import java.util.concurrent.locks.Lock;
import java.util.concurrent.locks.ReadWriteLock;
import java.util.concurrent.locks.ReentrantReadWriteLock;
 
class Sample {
	
    private int x;
	
    // ReadWriteLock object for requesting the lock.
    ReadWriteLock rw_lock = new ReentrantReadWriteLock();
 
    public int getX() {
        return x;
    }
 
    public void setX(int x) {
	this.x = x;
    }
	
    public void incr() {
		
	// Request the write lock as the 
	// operation is intended to modify the data.
 
	Lock lock = rw_lock.writeLock();                   //aquiring lock using writeLock
	lock.lock();
 
	try {
		
	    int y = getX();
	    y++;
			
	    // Just for simulation
	    try { Thread.sleep(1); } catch(Exception e) {}
			
	    setX(y);
 
	} finally {
	    // Unlock 
	    lock.unlock();              //releasing lock
	}	
    }
	
}
 
class MyThread extends Thread {
	
    Sample obj;
	
    public MyThread(Sample obj) {
	this.obj = obj;
    }
	
    public void run() {
	obj.incr();
    }	
}
 
public class Main {
 
    public static void main(String[] args) {
	Sample obj = new Sample();
	obj.setX(10);	
	MyThread t1 = new MyThread(obj);
	MyThread t2 = new MyThread(obj);	
	t1.start();
	t2.start();		
	try {
	    t1.join();
	    t2.join();
	} catch (InterruptedException e) {
	    e.printStackTrace();
	}
		
	System.out.println( obj.getX() );	
    }
}

```

### PRODUCER-CONSUMER PROBLEM - wait-notify example
```
import java.util.ArrayList;
import java.util.List;
 
class MessageQueue {
	
    List<String> messages;
    int limit;
	
    public MessageQueue(int limit) {
	messages = new ArrayList<String>();
	this.limit = limit;
    }
	
    public boolean isFull() {
	return messages.size() == limit;
    }
	
    public boolean isEmpty() {
	return messages.size() == 0;
    }
	
    public synchronized void enqueue(String msg) {
		
	while (isFull()) {
	    try {
		this.wait();
	    } catch (InterruptedException e) {
		e.printStackTrace();
	    }
	}
		
	messages.add(msg);
	this.notify();	
    }
	
    public synchronized String dequeue() {
		
	while (isEmpty()) {
	    try {
		this.wait();
	    } catch (InterruptedException e) {
	        e.printStackTrace();
	    }
	}
		
	String message = messages.remove(0);
	this.notify();
	return message;
    }
	
}
 
class ProducerThread extends Thread {
    MessageQueue queue;
	
    public ProducerThread(MessageQueue queue) {
	this.queue = queue;
    }	
    @Override
    public void run() {
	for(int i=1; i <= 10; i++) {
	    String msg = "Hello-" + i;
	    queue.enqueue(msg);
	    System.out.println("Produced - " + msg);
	}
    }
}
 
class ConsumerThread extends Thread {
    MessageQueue queue;
	
    public ConsumerThread(MessageQueue queue) {
	this.queue = queue;
    }	
    @Override
    public void run() {
	for(int i=1; i<=10; i++) {
	    String message = queue.dequeue();
	    System.out.println("Consumed - " + message);
	}
    }
}
 
public class Main {
    public static void main(String[] args) throws InterruptedException {
	MessageQueue queue = new MessageQueue(1);
	new ProducerThread(queue).start();
	new ConsumerThread(queue).start();
    }
}
```
### PRODUCER-CONSUMER problem with Blocking queue
BlockingQueue is an interface that extends Queue interface. And the implementations classes - 
1. ArrayBlockingQueue - It is bounded i.e. you need to specify the size. operate on FIFO logic i.e. first in first out, which means that the first inserted element will be the first to be removed.
2. LinkedBlockingQueue - Optionally Bounded, based on linked nodes i.e. nothing but the linked list. It too operates on FIFO logic.
3. PriorityBlockingQueue - Unbounded. Objects should be Comparable or you should provide a Comparator.

BlockingQueue operations
#### Operations that throw Exception if the operation fails.
1. add(o) - It tries to add an element and if there is no sufficient capacity available this method will throw an exception.
2. remove(o) - Removes the element that matches with the given object it compares the elements using equals method.
3. element() - Returns the head element with out removing it. But element() method throws an exception if queue is empty

#### Operations that return a boolean value with out exception

1. offer(o) - Returns true if the element is added otherwise false.
2. poll() - Removes the head element of the queue and returns it, if queue is empty it returns null.
3. peek() - Returns the head element with out removing it, it returns null if queue is empty.

#### Operations that block.
1. put(o) - It will add the element to the queue, but if the queue is full, then it will block the thread till the space is available.
2. take() - Returns the head element of the queue, if queue is empty this method will block the thread till an element is available.

#### And the methods with timeout
1. offer(o, timeout, timeunit)
2. poll(timeout, timeunit)

example
```
import java.util.concurrent.ArrayBlockingQueue;
import java.util.concurrent.BlockingQueue;

class ProducerThread extends Thread {
    BlockingQueue<String> queue;
	
    public ProducerThread(BlockingQueue<String>  queue) {
	this.queue = queue;
    }
	
    @Override
    public void run() {
	for(int i=1; i <= 10; i++) {
	    String msg = "Hello-" + i;
            
            // Blocks the thread until the space is available.
	    try {
		queue.put(msg);
                System.out.println("Produced - " + msg);
	    } catch (InterruptedException e) {
		e.printStackTrace();
	    }
	   
	}
    }
}
 
class ConsumerThread extends Thread {
    BlockingQueue<String> queue;
	
    public ConsumerThread(BlockingQueue<String> queue) {
	this.queue = queue;
    }
	
    @Override
    public void run() {
        for(int i=1; i<=10; i++) {
	    String message = null;
 
            // Blocks the thread until the element is available.
	    try {
		message = queue.take();
                System.out.println("Consumed - " + message);
	    } catch (InterruptedException e) {
		e.printStackTrace();
	    }
	    
	}
    }
}
 
public class Main {
    public static void main(String[] args) throws InterruptedException {
	BlockingQueue<String> queue = new ArrayBlockingQueue<String>(1);
	new ProducerThread(queue).start();
	new ConsumerThread(queue).start();
    }
}
```
 




