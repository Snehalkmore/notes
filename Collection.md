## Collection

### 1. ArrayList (default size =10)
1. implements List, RandomAccess,Clonable,Serializable interface and abstractList extended
2. Internally uses Array data structure of resizing.
3. Memory allocation would be continuous
4. Preserves insertion order
5. null and duplicate values allowed
6. Not synchronized
7. better perform for accessing and seach operation
8. Methods
```
add(),remove(),set(int index, Object o),get(index or object)
```


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
6. methods
```
add(),remove(),poll(),pollFist(),pollLat(), remove(), removeFirst(),removeLast(),peek(),peekFirst()
```
```
LinkedList<String> linkedlist = new LinkedList<String>();
    linkedlist.add("Delhi");
    linkedlist.add("Agra");

    ListIterator listIt = linkedlist.listIterator(); \\.................listIterator()
 
    // Iterating the list in forward direction
    while(listIt.hasNext()){
       System.out.println(listIt.next());
    }

    // Iterating the list in backward direction
    while(listIt.hasPrevious()){
       System.out.println(listIt.previous());
    } 
```



### 4. Vector
1. it is legacy class
2. it is synchronized
3. implements List, RandomAccess,Clonable,Serializable interface and abstractList extended
4. poor performance in searching, adding, delete and update of its elements.



### 5. HashSet (default size =16)
1. HashSet internally uses Hashtable data structure. 
2. PRESENT value (key would be inputed value to add and value would be PRESENT)
3. HashSet doesn’t maintain any order, the elements would be returned in any random order.
4. HashSet doesn’t allow duplicates. If you try to add a duplicate element in HashSet, the old value would be overwritten.
5. HashSet allows null values, however if you insert more than one nulls, it would override the previous null value.
6. HashSet is non-synchronized. However it can be synchronized explicitly like this:
   ```
   Set s = Collections.synchronizedSet(new HashSet(...));
   ```
7. The iterator returned by this class is fail-fast which means iterator would throw ConcurrentModificationException, if HashSet has been modified after creation of iterator, by any means except iterator’s own remove method.
```
 methods - add(), clear(), clone(), contains(), isEmpty()
```


### 6. LinkedHashSet
1. LinkedHashSet maintains the insertion order.
```
 methods - add(), clear(), clone(), contains(), isEmpty()
```

### 7. TreeSet 
1. it sorts the elements in the ascending order
2. It does not allow null value
3. non synchronized
```
 methods - add(), clear(), clone(), contains(), isEmpty()
```
