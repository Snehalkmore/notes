## Collection

### 1. ArrayList
1. implements List, RandomAccess,Clonable,Serializable interface and abstractClass extended
2. Preserves insertion order
3. null and duplicate values allowed
4. Not synchronized

### 2. How to make arrayList synchronized ??

1. we can use Collections.synchronized
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

### 3. 
