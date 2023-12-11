## Collection

### 1. ArrayList
1. implements List, RandomAccess,Clonable,Serializable interface and abstractClass extended
2. Internally uses Array data structure of resizing.
3. Memory allocation would be continuous
4. Preserves insertion order
5. null and duplicate values allowed
6. Not synchronized
7. better perform for accessing and seach operation

### 2. How to make arrayList synchronized ??

1. we can use Collections.synchronized(list)
```
public static void main(String a[]){
       List<String> syncal = 
         Collections.synchronizedList(new ArrayList<String>()); \\.........Collections.synchronizedList(list)

       //Adding elements to synchronized ArrayList
       syncal.add("Pen");
       syncal.add("NoteBook");
       syncal.add("Ink");

       System.out.println("Iterating synchronized ArrayList:");
       synchronized(syncal) {                             \\...........synchronized block
       Iterator<String> iterator = syncal.iterator(); 
       while (iterator.hasNext())
          System.out.println(iterator.next());
       }
   }
```

2. CopyOnWriteArrayList class - internally uses lock
```
final transient Object lock = new Object();

 synchronized (lock) {...}
```
```
public static void main(String a[]){
    CopyOnWriteArrayList<String> al = new CopyOnWriteArrayList<String>();

    //Adding elements to synchronized ArrayList
    al.add("Pen");
    al.add("NoteBook");
    al.add("Ink");

    System.out.println("Displaying synchronized ArrayList Elements:");
    //Synchronized block is not required in this method
    Iterator<String> iterator = al.iterator(); 
    while (iterator.hasNext())
       System.out.println(iterator.next());
  }
```

### 3. LinkedList
1. linkedList implements List, Deque, Clonable, Serialzable interfaces and extends AbstractSequentialList class
2. Internally uses linkedList datastructure
3. Stores data in combination of data and referance to next node format
4. Better perform in case of manipulation of list
5. Non synchronized
```
LinkedList<String> linkedlist = new LinkedList<String>();
    linkedlist.add("Delhi");
    linkedlist.add("Agra");

    ListIterator listIt = linkedlist.listIterator();
 
    // Iterating the list in forward direction
    while(listIt.hasNext()){
       System.out.println(listIt.next());
    }

    // Iterating the list in backward direction
    while(listIt.hasPrevious()){
       System.out.println(listIt.previous());
    } 
```

