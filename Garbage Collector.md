## Types of Garbage Collection
There are five types of garbage collection are as follows:

### Serial GC: 
It uses the mark and sweeps approach for young and old generations, which is minor and major GC.

### Parallel GC: 
It is similar to serial GC except that, it spawns N (the number of CPU cores in the system) threads for young generation garbage collection.

### Parallel Old GC:
It is similar to parallel GC, except that it uses multiple threads for both generations.

### Concurrent Mark Sweep (CMS) Collector: 
It does the garbage collection for the old generation. You can limit the number of threads in CMS collector using XX:ParalleCMSThreads=JVM option. It is also known as Concurrent Low Pause Collector.

### G1 Garbage Collector: 
It introduced in Java 7. Its objective is to replace the CMS collector. It is a parallel, concurrent, and CMS collector. There is no young and old generation space. It divides the heap into several equal-sized heaps. It first collects the regions with lesser live data.



## Memory heap generations
To fully understand how Java garbage collection works, it’s important to know about the different generations in the memory heap, which help make garbage collection more efficient. These generations are split into these types of spaces:

Eden: The eden space in Java is a memory pool where objects are created. When the eden space is full, the garbage collector either removes objects if they are no longer in use or stores them in the survivor space if they are still being used. This space is considered part of the young generation in the memory heap.
Survivor: There are two survivor spaces in the JVM: survivor zero and survivor one. This space is also part of the young generation.
Tenured: The tenured space is where long-lived objects are stored. Objects are eventually moved to this space if they survive a certain number of garbage collection cycles. This space is much larger than the eden space and the garbage collector checks it less often. This space is considered the old generation in the heap.


## Serial garbage collector
The serial garbage collector is typically used for smaller, single-threaded environments. Don’t use it in a production environment because the process of garbage collection takes over the thread, freezing other processes. This is known as a “stop the world” event.

## Parallel garbage collector
The parallel garbage collector is JVM’s default garbage collector. As the name implies this garbage collector uses multiple (parallel) threads. Because it can also use multiple CPUs to speed up throughput, it’s also known as the throughput collector. However, when running garbage collection, it will also freeze application threads.

## Garbage first (G1) garbage collector
The G1 garbage collector takes a different approach altogether. Instead of collecting the young and old generations separately, it can collect both at once by splitting the heap into many spaces—not just the eden, survivor, and tenured spaces that other garbage collectors use. This allows it to clear smaller regions instead of clearing large regions all at once, optimizing the collection process. It runs concurrently like the CMS collector, but it very rarely freezes execution and can collect both the young and old generations concurrently.




https://newrelic.com/blog/best-practices/java-garbage-collection#:~:text=During%20the%20garbage%20collection%20process,up%20memory%20in%20the%20heap.
