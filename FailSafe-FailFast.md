## FAIL SAFE vs FAIL FAST

<img width="529" alt="image" src="https://github.com/Snehalkmore/notes/assets/14993594/a0c2d2cf-6f47-48bf-9ea2-8d2166f27535">



### Fail fast Iterator

Fail fast iterator while iterating through the collection , instantly throws Concurrent Modification Exception if there is structural modification  of the collection . Thus, in the face of concurrent modification, the iterator fails quickly and cleanly, rather than risking arbitrary, non-deterministic behavior at an undetermined time in the future.

```
import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;

public class FailFastExample
{
    
    
    public static void main(String[] args)
    {
        Map<String,String> premiumPhone = new HashMap<String,String>();
        premiumPhone.put("Apple", "iPhone");
        premiumPhone.put("HTC", "HTC one");
        premiumPhone.put("Samsung","S5");
        
        Iterator iterator = premiumPhone.keySet().iterator();
        
        while (iterator.hasNext())
        {
            System.out.println(premiumPhone.get(iterator.next()));
            premiumPhone.put("Sony", "Xperia Z");
        }
        
    }
    
}
```

### How  Fail  Fast Iterator  come to know that the internal structure is modified ?
Iterator read internal data structure (object array) directly . The internal data structure(i.e object array) should not be modified while iterating through the collection. To ensure this it maintains an internal  flag "mods" .Iterator checks the "mods" flag whenever it gets the next value (using hasNext() method and next() method). Value of mods flag changes whenever there is an structural modification. Thus indicating iterator to throw ConcurrentModificationException.



### Fail Safe Iterator :

Fail Safe Iterator makes copy of the internal data structure (object array) and iterates over the copied data structure.Any structural modification done to the iterator affects the copied data structure.  So , original data structure remains  structurally unchanged .Hence , no ConcurrentModificationException throws by the fail safe iterator.

Two  issues associated with Fail Safe Iterator are :
1. Overhead of maintaining the copied data structure i.e memory.
2.  Fail safe iterator does not guarantee that the data being read is the data currently in the original data structure.

```
import java.util.concurrent.ConcurrentHashMap;
import java.util.Iterator;
public class FailSafeExample
{   
    public static void main(String[] args)
    {
        ConcurrentHashMap<String,String> premiumPhone = 
                               new ConcurrentHashMap<String,String>();
        premiumPhone.put("Apple", "iPhone");
        premiumPhone.put("HTC", "HTC one");
        premiumPhone.put("Samsung","S5");
        
        Iterator iterator = premiumPhone.keySet().iterator();
        
        while (iterator.hasNext())
        {
            System.out.println(premiumPhone.get(iterator.next()));
            premiumPhone.put("Sony", "Xperia Z");
        }
        
    }
    
}
```


