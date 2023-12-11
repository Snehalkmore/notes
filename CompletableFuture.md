## CompletableFuture

1. A CompltableFuture is used for asynchronous programming. Asynchronous programming means writing non-blocking code.
2. It runs a task on a separate thread than the main application thread and notifies the main thread about its progress, completion or failure.
3. In this way, the main thread does not block or wait for the completion of the task. Other tasks execute in parallel. Parallelism improves the performance of the program.
4. A CompletableFuture is a class in Java. It belongs to java.util.cocurrent package. It implements CompletionStage and Future interface.



## Future
A Future is used for asynchronous Programming. It provides two methods, isDone() and get(). The methods retrieve the result of the computation when it completes.

## Limitation of Future
1. A Future cannot be mutually complete.
2. We cannot perform further action on a Future's result without blocking.
3. Future has not any exception handling.
4. We cannot combine multiple futures.

Syntax
```
CompletableFuture<String> CompletableFuture = new CompletableFuture<String>();  
```

### Methods from 
1. supplyAsync(): It complete its job asynchronously. The result of SUPLIER interface is run by a task from ForkJoinPool.commonPool() as default. The supplyAsync() method returns CompletableFuture on which we can apply other methods.
2. thenApply(): The method accepts Function as an arguments. It returns a new CompletableStage when this stage completes normally. The new stage use as the argument to the supplied function.
3. join(): the method returns the result value when complete. It also throws a CompletionException (unchecked exception) if completed exceptionally.

```
import java.util.concurrent.CompletableFuture;  
public class CompletableFutureExample1 {  
    public static void main(String[] args)   
    {  
      try {  
        List<Integer> list = Arrays.asList(5,9,14);  
          list.stream()
            .map(num->CompletableFuture.supplyAsync(()->getNumber(num)))
            .map(CompletableFuture->CompletableFuture.thenApply(n->n*n))
            .map(t->t.join())
            .forEach(s->System.out.println(s));  
          } catch (Exception e)  { e.printStackTrace(); }  
    }  
    private static int getNumber(int a) {  
        return a*a;  
  }
}  
```


